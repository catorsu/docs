# search

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/search
- **Version**: Current as of June 2025

## Overview

Use the search API to retrieve the installed search engines and execute searches. This API provides functionality to get information about available search engines and perform searches using them.

When choosing between search.query() and search.search(), consider that query() is available in most major browsers but can only search against the default search engine, while search() is Firefox-only but can search against any installed search engine.

## Permissions
- `search` - required to use this API

## Types

### SearchEngine
Represents a search engine with the following properties:
- **name**: string - Display name of the search engine
- **isDefault**: boolean - Whether this is the default search engine
- **alias**: string - Keyword alias for the search engine (optional)
- **favIconUrl**: string - URL of the search engine's favicon (optional)

## Methods

### get()
**Syntax**: `browser.search.get()`

Retrieve all search engines available in the browser.

#### Parameters
None.

#### Returns
- **Type**: `Promise<array>`
- **Description**: Promise that resolves to an array of SearchEngine objects

#### Code Examples
```javascript
browser.search.get().then(engines => {
  engines.forEach(engine => {
    console.log(`Engine: ${engine.name}, Default: ${engine.isDefault}`);
  });
});
```

### query()
**Syntax**: `browser.search.query(queryInfo)`

Search using the browser's default search engine. Available in most major browsers.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| queryInfo | object | Yes | - | Search query details |
| queryInfo.text | string | Yes | - | Search query text |
| queryInfo.disposition | string | No | "CURRENT_TAB" | Where to display results ("CURRENT_TAB", "NEW_TAB", "NEW_WINDOW") |
| queryInfo.tabId | number | No | - | Tab ID to perform search in (for "CURRENT_TAB" disposition) |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when search is initiated

#### Code Examples
```javascript
// Search in current tab
browser.search.query({
  text: "WebExtensions"
});

// Search in new tab
browser.search.query({
  text: "Firefox extensions",
  disposition: "NEW_TAB"
});
```

### search()
**Syntax**: `browser.search.search(searchProperties)`

Search using a specified search engine. Available only in Firefox.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| searchProperties | object | Yes | - | Search properties |
| searchProperties.query | string | Yes | - | Search query text |
| searchProperties.engine | string | No | - | Name of search engine to use (uses default if omitted) |
| searchProperties.disposition | string | No | "CURRENT_TAB" | Where to display results |
| searchProperties.tabId | number | No | - | Tab ID for search (for "CURRENT_TAB" disposition) |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when search is initiated

#### Code Examples
```javascript
// Search using specific engine
browser.search.search({
  query: "JavaScript tutorials",
  engine: "Google"
});

// Search using default engine in new window
browser.search.search({
  query: "MDN WebExtensions",
  disposition: "NEW_WINDOW"
});
```

## Events
No events are defined for this API.

## Related APIs
- `tabs` - For managing tabs where search results are displayed
- `omnibox` - For creating custom address bar search functionality
- `contextMenus` - For adding search options to context menus
