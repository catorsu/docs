# Find

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/find
- **Version**: Firefox 57+

## Overview
Finds text in a web page, and highlights matches. This API allows extensions to programmatically search for text within web pages and highlight the results.

The API stores search results internally, and any extension calling highlightResults() will highlight the results from the most recent find() call across all extensions.

## Permissions
- `find` - required

## Types
### RangeData
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| frameId | integer | Yes | - | The frame ID where the match was found |
| startOffset | integer | Yes | - | The start offset within the text node |
| endOffset | integer | Yes | - | The end offset within the text node |
| startTextNodePos | integer | Yes | - | Ordinal position of the start text node |
| endTextNodePos | integer | Yes | - | Ordinal position of the end text node |

### RectData  
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| rectsAndTexts | object | Yes | - | Contains rectangle and text information |
| rectsAndTexts.rectList | Array<object> | Yes | - | Array of DOMRect-like objects |
| rectsAndTexts.textList | Array<string> | Yes | - | Array of text strings within the rectangles |

### FindResult
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| count | integer | Yes | - | Number of matches found |
| rangeData | Array<RangeData> | No | - | Range data if includeRangeData was true |
| rectData | Array<RectData> | No | - | Rectangle data if includeRectData was true |

## Methods
### find()
**Syntax**: `browser.find.find(searchString, options)`

Searches for text in a tab. Searches all frames in the tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| searchString | string | Yes | - | The string to search for |
| options | object | No | {} | Search options |
| options.tabId | integer | No | Active tab | Tab to search in |
| options.caseSensitive | boolean | No | false | Whether the search is case sensitive |
| options.entireWord | boolean | No | false | Match only entire words |
| options.includeRangeData | boolean | No | false | Include range data in results |
| options.includeRectData | boolean | No | false | Include rectangle data in results |

#### Returns
- **Type**: `Promise<FindResult>`
- **Description**: Object containing search results

#### Code Examples
```javascript
function found(results) {
  console.log(`There were: ${results.count} matches.`);
  if (results.count > 0) {
    browser.find.highlightResults();
  }
}

browser.find.find("banana").then(found);

// Search across all tabs
async function findInAllTabs(allTabs) {
  for (const tab of allTabs) {
    const results = await browser.find.find("banana", { tabId: tab.id });
    console.log(`In page "${tab.url}": ${results.count} matches.`);
  }
}

browser.tabs.query({}).then(findInAllTabs);

// Using rectangle data to redact matches
browser.find.find("secret", {
  includeRectData: true
}).then((results) => {
  if (results.count > 0) {
    browser.tabs.executeScript({
      code: `(${redactMatches})(${JSON.stringify(results.rectData)})`
    });
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/find/find

### highlightResults()
**Syntax**: `browser.find.highlightResults(options)`

Highlights the results of a previous call to find.find(). Note that the stored results are global across all extensions.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | No | {} | Highlighting options |
| options.rangeIndex | integer | No | All ranges | Specific range to highlight |
| options.tabId | integer | No | Active tab | Tab to highlight in |
| options.noScroll | boolean | No | false | Don't scroll to highlighted item |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with count property

#### Code Examples
```javascript
function found(results) {
  console.log(`There were: ${results.count} matches.`);
  if (results.count > 0) {
    browser.find.highlightResults();
  }
}

browser.find.find("banana").then(found);

// Highlight specific range
browser.find.find("example").then((results) => {
  if (results.count > 0) {
    browser.find.highlightResults({
      rangeIndex: 0,  // Highlight first match only
      noScroll: true
    });
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/find/highlightResults

### removeHighlighting()
**Syntax**: `browser.find.removeHighlighting(tabId)`

Remove any highlighting of a previous search that was applied by highlightResults() or by the browser's native UI.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | No | Active tab | Tab to remove highlighting from |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when highlighting is removed

#### Code Examples
```javascript
// Remove highlighting from the active tab
browser.find.removeHighlighting();

// Remove highlighting from a specific tab
browser.find.removeHighlighting(tabId);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/find/removeHighlighting

## Events
None

## Related APIs
- `tabs` - For specifying which tab to search in
- `scripting` - For injecting scripts to process search results