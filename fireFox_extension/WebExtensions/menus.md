# menus

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/menus
- **Version**: WebExtensions API

## Overview

Add items to the browser's menu system. This API is modeled on Chrome's "contextMenus" API, which enables extensions to add items to the browser's context menu. The `browser.menus` API adds a few features to Chrome's API.

Before Firefox 55 this API was originally named `contextMenus`, and that name has been retained as an alias. You can use `contextMenus` to write code that works in Firefox and other browsers.

**Key Features**:
- Create context menu items for various contexts (page, image, link, etc.)
- Create checkbox and radio button menu items
- Organize items in submenus
- Add items to browser action, page action, and tools menus
- Override default context menus in extension pages

## Permissions
- `menus` - required (or `contextMenus` alias)
- Cannot be used from content scripts (except `getTargetElement()`)

## Types

### ContextType
The different contexts a menu item can appear in.

| Value | Description |
|-------|-------------|
| `"all"` | Combination of all contexts except 'bookmark', 'tab' and 'tools_menu' |
| `"action"` | Browser action context menu (Manifest V3) |
| `"audio"` | Context menu on an audio element |
| `"bookmark"` | Bookmark item in toolbar, menu, sidebar, or Library window |
| `"browser_action"` | Browser action context menu (Manifest V2) |
| `"editable"` | Editable element like textarea |
| `"frame"` | Nested iframe |
| `"image"` | Context menu on an image |
| `"link"` | Context menu on a link |
| `"page"` | Page context, but not on any specific element |
| `"page_action"` | Page action context menu |
| `"password"` | Password input field |
| `"selection"` | When text is selected |
| `"tab"` | Tab context menu (requires "tabs" permission) |
| `"tools_menu"` | Browser's tools menu |
| `"video"` | Context menu on a video element |

### ItemType
The type of menu item.

| Value | Description |
|-------|-------------|
| `"normal"` | Menu item that just displays a label |
| `"checkbox"` | Menu item representing a binary state with checkmark |
| `"radio"` | Menu item representing one of a group of choices |
| `"separator"` | Line separating a group of items |

### OnClickData
Information passed when a menu item is clicked.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `bookmarkId` | string | No | ID of bookmark where context menu was clicked |
| `button` | integer | No | Which mouse button was used (0=left, 1=middle, 2=right) |
| `checked` | boolean | No | Whether checkbox/radio is now checked |
| `editable` | boolean | Yes | Whether element is editable |
| `frameId` | integer | No | ID of frame where item was clicked |
| `frameUrl` | string | No | URL of the frame |
| `linkText` | string | No | Text of the link (if on a link) |
| `linkUrl` | string | No | URL of the link |
| `mediaType` | string | No | "image", "video", or "audio" |
| `menuItemId` | integer/string | Yes | ID of the clicked menu item |
| `modifiers` | array of string | Yes | Keyboard modifiers: "Alt", "Command", "Ctrl", "MacCtrl", "Shift" |
| `pageUrl` | string | No | URL of the page |
| `parentMenuItemId` | integer/string | No | Parent menu item ID |
| `selectionText` | string | No | Selected text |
| `srcUrl` | string | No | Source URL of media element |
| `targetElementId` | integer | No | ID of element where context menu was opened |
| `viewType` | string | No | Type of view: "tab", "popup", "sidebar" |
| `wasChecked` | boolean | No | Whether checkbox/radio was checked before |

## Properties

### ACTION_MENU_TOP_LEVEL_LIMIT
Maximum number of top-level extension items for action context menus.

- **Type**: `integer`
- **Value**: `6`
- **Applies to**: `"browser_action"`, `"page_action"`, `"action"` contexts

## Methods

### create()
Creates a new menu item.

**Syntax**: `browser.menus.create(createProperties, callback)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `createProperties` | object | Yes | - | Properties for the menu item |
| `createProperties.checked` | boolean | No | false | Initial state of checkbox/radio |
| `createProperties.command` | string | No | - | Keyboard shortcut description |
| `createProperties.contexts` | array | No | ["page"] | Array of ContextTypes |
| `createProperties.documentUrlPatterns` | array | No | - | Restrict to matching document URLs |
| `createProperties.enabled` | boolean | No | true | Whether item is enabled |
| `createProperties.icons` | object | No | - | Custom icons for submenus |
| `createProperties.id` | string | No | - | Unique ID for the item |
| `createProperties.parentId` | string/integer | No | - | ID of parent item |
| `createProperties.targetUrlPatterns` | array | No | - | Restrict to matching target URLs |
| `createProperties.title` | string | No | - | Text displayed in item |
| `createProperties.type` | ItemType | No | "normal" | Type of menu item |
| `createProperties.viewTypes` | array | No | - | List of view types |
| `createProperties.visible` | boolean | No | true | Whether item is visible |
| `callback` | function | No | - | Called when item is created |

**Note**: In Firefox with non-persistent background pages or Chrome, call from `runtime.onInstalled`. In Firefox with persistent background pages, make a top-level call.

#### Returns
- **Type**: `integer` or `string`
- **Description**: The ID of the newly created item

#### Code Examples
```javascript
// Simple context menu item
browser.menus.create({
  id: "log-selection",
  title: "Log '%s' to console",
  contexts: ["selection"]
});

// Radio items with custom icons
browser.menus.create({
  id: "greenify",
  type: "radio",
  title: "Make it green",
  contexts: ["all"],
  checked: true,
  icons: {
    "16": "icons/paint-green-16.png",
    "32": "icons/paint-green-32.png"
  }
});

// Checkbox item
browser.menus.create({
  id: "toggle-feature",
  type: "checkbox",
  title: "Enable feature",
  contexts: ["page"],
  checked: false
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/menus/create

### update()
Updates a previously created menu item.

**Syntax**: `browser.menus.update(id, updateProperties)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `id` | integer/string | Yes | ID of item to update |
| `updateProperties` | object | Yes | Properties to update (same as create) |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when update completes

#### Code Examples
```javascript
browser.menus.update("my-item", {
  title: "New title",
  enabled: false
});
```

### remove()
Removes a menu item.

**Syntax**: `browser.menus.remove(menuItemId)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `menuItemId` | integer/string | Yes | ID of item to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when item is removed

#### Code Examples
```javascript
browser.menus.remove("my-item").then(() => {
  console.log("Item removed");
});
```

### removeAll()
Removes all menu items added by this extension.

**Syntax**: `browser.menus.removeAll()`

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when all items are removed

### getTargetElement()
Returns the element for a given `targetElementId`.

**Syntax**: `browser.menus.getTargetElement(targetElementId)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `targetElementId` | integer | Yes | ID from OnClickData |

#### Returns
- **Type**: `Element` or `null`
- **Description**: The element, if found and still exists

**Note**: Can be called from content scripts

### overrideContext()
Hide all default Firefox menu items in favor of custom context menu.

**Syntax**: `browser.menus.overrideContext(contextOptions)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `contextOptions` | object | Yes | Override options |
| `contextOptions.context` | string | No | "bookmark" or "tab" |
| `contextOptions.showDefaults` | boolean | No | Include default items |
| `contextOptions.bookmarkId` | string | No | Required when context is "bookmark" |
| `contextOptions.tabId` | integer | No | Required when context is "tab" |

**Note**: Call from a `contextmenu` DOM event handler

#### Code Examples
```javascript
document.addEventListener("contextmenu", (event) => {
  const foo = event.target.closest(".foo");
  if (foo) {
    browser.menus.overrideContext({
      context: "tab",
      tabId: parseInt(foo.dataset.tabId)
    });
  }
}, { capture: true });
```

### refresh()
Updates the extension's menu items in the currently shown menu.

**Syntax**: `browser.menus.refresh()`

**Note**: Rebuilding a shown menu is expensive, use sparingly

## Events

### onClicked
Fired when a menu item is clicked.

**Syntax**: `browser.menus.onClicked.addListener(listener)`

**Listener receives**:
- `info` (OnClickData): Information about the click
- `tab` (tabs.Tab): The tab where click occurred (not in all contexts)

#### Code Examples
```javascript
browser.menus.onClicked.addListener((info, tab) => {
  switch (info.menuItemId) {
    case "log-selection":
      console.log("Selected text: " + info.selectionText);
      break;
    case "remove-me":
      browser.menus.remove(info.menuItemId);
      break;
  }
});
```

### onShown
Fired when the browser shows a menu.

**Syntax**: `browser.menus.onShown.addListener(listener)`

**Listener receives**:
- `info` (object): Information about the shown menu
  - `contexts`: Array of all contexts that apply
  - `menuIds`: Array of IDs of all visible menu items
  - `editable`: Boolean indicating if context is editable
  - `mediaType`: "image", "video", or "audio" if applicable
  - `targetElementId`: ID that can be used with getTargetElement()

### onHidden
Fired when the browser hides a menu.

**Syntax**: `browser.menus.onHidden.addListener(listener)`

**Listener receives**: No parameters

## Usage Examples

### Complete Context Menu System
```javascript
// Create a context menu with multiple items
function onCreated() {
  if (browser.runtime.lastError) {
    console.log("Error:", browser.runtime.lastError);
  }
}

// Parent menu item
browser.menus.create({
  id: "tools-menu",
  title: "My Tools",
  contexts: ["all"]
}, onCreated);

// Child items
browser.menus.create({
  id: "tool-1",
  parentId: "tools-menu",
  title: "Tool 1",
  contexts: ["all"]
}, onCreated);

// Separator
browser.menus.create({
  id: "separator-1",
  parentId: "tools-menu",
  type: "separator",
  contexts: ["all"]
}, onCreated);

// Radio group
browser.menus.create({
  id: "radio-1",
  parentId: "tools-menu",
  type: "radio",
  title: "Option 1",
  contexts: ["all"],
  checked: true
}, onCreated);

browser.menus.create({
  id: "radio-2",
  parentId: "tools-menu",
  type: "radio",
  title: "Option 2",
  contexts: ["all"]
}, onCreated);

// Handle clicks
browser.menus.onClicked.addListener((info, tab) => {
  console.log("Clicked:", info.menuItemId);
  console.log("Info:", info);
  if (tab) {
    console.log("Tab:", tab.id);
  }
});
```

### Dynamic Menu Updates
```javascript
// Update menu based on context
browser.menus.onShown.addListener(async (info) => {
  if (info.contexts.includes("selection")) {
    await browser.menus.update("process-text", {
      title: `Process "${info.selectionText.substring(0, 15)}..."`
    });
  }
  await browser.menus.refresh();
});

// Clean up when menu is hidden
browser.menus.onHidden.addListener(() => {
  console.log("Menu hidden");
});
```

### Context-Specific Menus
```javascript
// Image context menu
browser.menus.create({
  id: "save-image",
  title: "Save image to...",
  contexts: ["image"],
  documentUrlPatterns: ["*://*/*"]
});

// Link context menu
browser.menus.create({
  id: "open-link",
  title: "Open link in container",
  contexts: ["link"],
  targetUrlPatterns: ["*://*.example.com/*"]
});

// Selection context menu with %s substitution
browser.menus.create({
  id: "search-selection",
  title: 'Search for "%s"',
  contexts: ["selection"]
});
```

## Manifest V2 vs V3 Differences

1. **Naming**: Use `menus` in Manifest V3, though `contextMenus` still works as alias
2. **Action contexts**: Use `"action"` in V3 instead of `"browser_action"` in V2
3. **Background scripts**: V3 uses service workers requiring menu creation in `runtime.onInstalled`

## Related APIs
- `tabs` - Get information about tabs in menu events
- `i18n` - Localize menu item titles
- `commands` - Define keyboard shortcuts for menu items
- `runtime` - Use onInstalled for menu creation in non-persistent contexts