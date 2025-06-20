# omnibox

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/omnibox
- **Version**: WebExtensions API

## Overview

Enables extensions to implement customized behavior when the user types into the browser's address bar. Extensions can provide custom suggestions in the address bar dropdown when the user types a specific keyword.

**How it works**:
1. Define a keyword in manifest.json using the "omnibox" key
2. When user types keyword + space, extension gets notified
3. Extension can set a default suggestion and provide custom suggestions
4. User selecting a suggestion triggers an event in the extension

## Permissions
No special permission required, but must include "omnibox" key in manifest.json

## Manifest Entry
```json
{
  "omnibox": {
    "keyword": "ext"
  }
}
```

## Types

### OnInputEnteredDisposition
Describes the recommended method to handle the selected suggestion.

| Value | Description |
|-------|-------------|
| `"currentTab"` | Open in the current tab |
| `"newForegroundTab"` | Open in a new foreground tab |
| `"newBackgroundTab"` | Open in a new background tab |

### SuggestResult
Defines a suggestion for the address bar dropdown.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `content` | string | Yes | - | Value that appears in address bar when highlighted |
| `description` | string | Yes | - | Text displayed in the dropdown list |
| `deletable` | boolean | No | false | Whether user can delete this suggestion |

**Notes**:
- `content` is sent to `onInputEntered` if user selects this suggestion
- If `content` equals what user already typed, suggestion won't appear
- `description` supports limited XML formatting:
  - `<match>` for highlighting matched text
  - `<url>` for URL styling
  - `<dim>` for dim text

## Methods

### setDefaultSuggestion()
Sets the first suggestion displayed in the dropdown when user types keyword + space.

**Syntax**: `browser.omnibox.setDefaultSuggestion(suggestion)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `suggestion` | object | Yes | Object with `description` property |
| `suggestion.description` | string | Yes | Text for default suggestion |

**Note**: Default suggestion cannot be selected, only used for guidance

#### Code Examples
```javascript
browser.omnibox.setDefaultSuggestion({
  description: "Search my bookmarks for '%s'"
});

// With formatting
browser.omnibox.setDefaultSuggestion({
  description: "Type to search <dim>example.com</dim>"
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/omnibox/setDefaultSuggestion

## Events

### onInputStarted
Fired when user focuses address bar and types keyword + space.

**Syntax**: `browser.omnibox.onInputStarted.addListener(listener)`

**Listener receives**: No parameters

#### Code Examples
```javascript
browser.omnibox.onInputStarted.addListener(() => {
  console.log("User started typing after keyword");
});
```

### onInputChanged
Fired whenever user's input changes after keyword + space.

**Syntax**: `browser.omnibox.onInputChanged.addListener(listener)`

**Listener receives**:
- `text` (string): Current user input (not including keyword)
- `suggest` (function): Callback to provide suggestions

#### Code Examples
```javascript
browser.omnibox.onInputChanged.addListener((text, suggest) => {
  // Create suggestions based on text
  const suggestions = [
    {
      content: "https://example.com/search?q=" + encodeURIComponent(text),
      description: `Search for <match>${text}</match> on Example.com`
    },
    {
      content: "https://docs.example.com/" + text,
      description: `Go to <url>docs.example.com/${text}</url>`
    }
  ];
  
  // Pass array to suggest callback (max 6 will be shown)
  suggest(suggestions);
});

// Async suggestion loading
browser.omnibox.onInputChanged.addListener(async (text, suggest) => {
  const results = await searchBookmarks(text);
  const suggestions = results.map(bookmark => ({
    content: bookmark.url,
    description: `<match>${bookmark.title}</match> - <dim>${bookmark.url}</dim>`
  }));
  suggest(suggestions);
});
```

### onInputEntered
Fired when user accepts a suggestion or presses Enter.

**Syntax**: `browser.omnibox.onInputEntered.addListener(listener)`

**Listener receives**:
- `text` (string): Either suggestion's `content` or user's input
- `disposition` (OnInputEnteredDisposition): How to open the URL

#### Code Examples
```javascript
browser.omnibox.onInputEntered.addListener((text, disposition) => {
  let url = text;
  
  // Check if user selected default suggestion (typed their own text)
  if (!text.startsWith("http")) {
    url = `https://example.com/search?q=${encodeURIComponent(text)}`;
  }
  
  // Handle based on user preference
  switch (disposition) {
    case "currentTab":
      browser.tabs.update({ url });
      break;
    case "newForegroundTab":
      browser.tabs.create({ url });
      break;
    case "newBackgroundTab":
      browser.tabs.create({ url, active: false });
      break;
  }
});
```

### onInputCancelled
Fired when user dismisses the address bar dropdown.

**Syntax**: `browser.omnibox.onInputCancelled.addListener(listener)`

**Listener receives**: No parameters

#### Code Examples
```javascript
browser.omnibox.onInputCancelled.addListener(() => {
  console.log("User cancelled omnibox input");
  // Clean up any resources
});
```

### onDeleteSuggestion
Fired when user deletes a suggestion (if `deletable: true`).

**Syntax**: `browser.omnibox.onDeleteSuggestion.addListener(listener)`

**Listener receives**:
- `text` (string): The suggestion's content that was deleted

#### Code Examples
```javascript
browser.omnibox.onDeleteSuggestion.addListener((text) => {
  console.log(`User deleted suggestion: ${text}`);
  // Remove from your data source
  removeFromHistory(text);
});
```

## Complete Example

### CSS Property Search
```javascript
// manifest.json
{
  "manifest_version": 2,
  "name": "CSS Property Search",
  "version": "1.0",
  "omnibox": {
    "keyword": "css"
  },
  "background": {
    "scripts": ["background.js"]
  }
}

// background.js
const CSS_PROPERTIES = [
  "animation", "background", "border", "box-shadow",
  "color", "display", "flex", "float", "font",
  "grid", "margin", "opacity", "overflow", 
  "padding", "position", "transform", "transition"
];

const MDN_BASE = "https://developer.mozilla.org/en-US/docs/Web/CSS/";

// Set default suggestion
browser.omnibox.setDefaultSuggestion({
  description: "Search CSS properties (e.g., 'display', 'flex')"
});

// Handle input changes
browser.omnibox.onInputChanged.addListener((text, suggest) => {
  const query = text.toLowerCase();
  
  // Filter matching properties
  const matches = CSS_PROPERTIES.filter(prop => 
    prop.toLowerCase().includes(query)
  );
  
  // Create suggestions
  const suggestions = matches.map(prop => ({
    content: MDN_BASE + prop,
    description: `<match>${prop}</match> - CSS property`,
    deletable: false
  }));
  
  suggest(suggestions);
});

// Handle selection
browser.omnibox.onInputEntered.addListener((text, disposition) => {
  let url = text;
  
  // If not a URL, search MDN
  if (!text.startsWith("http")) {
    url = `${MDN_BASE}?search=${encodeURIComponent(text)}`;
  }
  
  // Open based on disposition
  if (disposition === "currentTab") {
    browser.tabs.update({ url });
  } else {
    browser.tabs.create({ 
      url, 
      active: disposition === "newForegroundTab" 
    });
  }
});
```

### Bookmark Search
```javascript
// Search bookmarks as user types
browser.omnibox.onInputChanged.addListener(async (text, suggest) => {
  if (!text) return;
  
  // Search bookmarks
  const bookmarks = await browser.bookmarks.search({ query: text });
  
  // Convert to suggestions
  const suggestions = bookmarks
    .filter(b => b.url) // Only items with URLs
    .slice(0, 6) // Limit to 6 suggestions
    .map(bookmark => ({
      content: bookmark.url,
      description: `<match>${bookmark.title}</match> - <url>${new URL(bookmark.url).hostname}</url>`
    }));
  
  suggest(suggestions);
});
```

### Command Palette
```javascript
const COMMANDS = {
  "new tab": () => browser.tabs.create({}),
  "downloads": () => browser.tabs.create({ url: "chrome://downloads" }),
  "settings": () => browser.runtime.openOptionsPage(),
  "clear data": () => browser.browsingData.remove({}, { history: true })
};

browser.omnibox.onInputChanged.addListener((text, suggest) => {
  const query = text.toLowerCase();
  
  const suggestions = Object.keys(COMMANDS)
    .filter(cmd => cmd.includes(query))
    .map(cmd => ({
      content: cmd,
      description: `<match>${cmd}</match> - Execute command`
    }));
  
  suggest(suggestions);
});

browser.omnibox.onInputEntered.addListener((text) => {
  const command = COMMANDS[text];
  if (command) {
    command();
  }
});
```

## Best Practices

1. **Performance**: Keep `onInputChanged` handler fast to avoid lag
2. **Debouncing**: Consider debouncing API calls in `onInputChanged`
3. **Suggestion Limit**: Only first 6 suggestions are shown
4. **Clear Descriptions**: Use formatting to highlight important parts
5. **Default Suggestion**: Provide helpful guidance about usage
6. **URL Handling**: Always validate/sanitize URLs before navigation

## Formatting Guide

Description text supports limited XML:
- `<match>text</match>` - Highlighted text (usually search matches)
- `<dim>text</dim>` - Dimmed text (for less important info)
- `<url>text</url>` - URL formatting

## Related APIs
- `bookmarks` - Search and access bookmarks
- `history` - Search browsing history
- `tabs` - Open URLs in tabs
- `storage` - Cache suggestions for performance