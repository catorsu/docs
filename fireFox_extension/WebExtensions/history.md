# history

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history
- **Version**: WebExtensions API

## Overview

Use the `history` API to interact with the browser history. Browser history is a chronological record of pages the user has visited. The history API enables you to search for pages in browser history, add/remove pages, delete visits, and monitor history changes. Downloads are treated as HistoryItem objects, so events like `history.onVisited` fire for downloads.

The API also has the concept of "visits" - a single page may be visited multiple times. You can retrieve all visits to a page or remove visits during a specific time period.

## Permissions
- `history` - required

## Types

### TransitionType
Describes how the browser navigated to a particular page.

| Value | Description |
|-------|-------------|
| `"link"` | The user clicked a link in another page |
| `"typed"` | The user typed the URL into the address bar or selected from suggestions |
| `"auto_bookmark"` | The user clicked a bookmark or an item in browser history |
| `"auto_subframe"` | Any nested iframes automatically loaded by their parent |
| `"manual_subframe"` | Nested iframes loaded as an explicit user action |
| `"generated"` | User typed in address bar and clicked on a suggested entry without URL |
| `"auto_toplevel"` | Page passed to command line or is the start page |
| `"form_submit"` | User submitted a form |
| `"reload"` | User reloaded the page (Reload button or Enter in address bar) |
| `"keyword"` | URL generated using a keyword search configured by the user |
| `"keyword_generated"` | Corresponds to a visit generated for a keyword |

### HistoryItem
Provides information about a page in the browser history.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `id` | string | Yes | - | Unique identifier for the item |
| `url` | string | No | - | The URL of the page |
| `title` | string | No | - | The title of the page |
| `lastVisitTime` | number | No | - | Date/time page was last loaded (milliseconds since epoch) |
| `visitCount` | number | No | - | Number of times user has visited the page |
| `typedCount` | number | No | - | Number of times user navigated to page by typing address |

### VisitItem
Describes a single visit to a page.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `id` | string | Yes | - | Unique identifier for the HistoryItem |
| `visitId` | string | Yes | - | Unique identifier for this visit |
| `visitTime` | number | No | - | When visit occurred (milliseconds since epoch) |
| `referringVisitId` | string | Yes | - | The visit ID of the referrer |
| `transition` | TransitionType | Yes | - | How browser navigated to page |

## Methods

### search()
Searches the browser's history for HistoryItem objects matching given criteria.

**Syntax**: `browser.history.search(query)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `query` | object | Yes | - | Search query object |
| `query.text` | string | No | "" | Search by URL and title (case-insensitive, space-separated terms) |
| `query.startTime` | number/string/Date | No | - | Limit results to visits after this time |
| `query.endTime` | number/string/Date | No | - | Limit results to visits before this time |
| `query.maxResults` | number | No | 100 | Maximum number of results to retrieve |

#### Returns
- **Type**: `Promise<HistoryItem[]>`
- **Description**: Array of matching HistoryItem objects sorted by recency

#### Code Examples
```javascript
function onGot(historyItems) {
  for (const item of historyItems) {
    console.log(item.url);
    console.log(new Date(item.lastVisitTime));
  }
}

browser.history.search({
  text: "mozilla",
  startTime: 0,
  maxResults: 1
}).then(onGot);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/search

### getVisits()
Retrieves information about all visits to the given URL.

**Syntax**: `browser.history.getVisits(details)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `details` | object | Yes | - | Object specifying the URL |
| `details.url` | string | Yes | - | The URL for which to retrieve visit information |

#### Returns
- **Type**: `Promise<VisitItem[]>`
- **Description**: Array of VisitItem objects in reverse chronological order

#### Code Examples
```javascript
function gotVisits(visits) {
  console.log("Visit count: " + visits.length);
  for (visit of visits) {
    console.log(visit.visitTime);
  }
}

function listVisits(historyItems) {
  if (historyItems.length) {
    console.log("URL " + historyItems[0].url);
    browser.history.getVisits({
      url: historyItems[0].url
    }).then(gotVisits);
  }
}

browser.history.search({
  text: "",
  startTime: 0,
  maxResults: 1
}).then(listVisits);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/getVisits

### addUrl()
Adds a record to the browser history of a visit to the given URL. Visit time is recorded as time of the call, TransitionType as "link".

**Syntax**: `browser.history.addUrl(details)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `details` | object | Yes | - | Object describing the URL to add |
| `details.url` | string | Yes | - | The URL to add |
| `details.title` | string | No | - | The title of the page |
| `details.transition` | TransitionType | No | "link" | How browser navigated to page |
| `details.visitTime` | number/string/Date | No | current time | When the visit occurred |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the item has been added

#### Code Examples
```javascript
function onGot(results) {
  if (results.length) {
    console.log("Added: " + results[0].url);
    console.log("Time: " + new Date(results[0].lastVisitTime));
  }
}

browser.history.addUrl({
  url: "https://example.org/"
}).then(() => {
  return browser.history.search({
    text: "https://example.org/",
    startTime: 0
  });
}).then(onGot);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/addUrl

### deleteUrl()
Removes all visits to the given URL from the browser history.

**Syntax**: `browser.history.deleteUrl(details)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `details` | object | Yes | - | Object specifying the URL |
| `details.url` | string | Yes | - | The URL to remove from history |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when visits have been removed

#### Code Examples
```javascript
function onGot(results) {
  if (results.length) {
    console.log("Removing: " + results[0].url);
    browser.history.deleteUrl({url: results[0].url});
  }
}

browser.history.search({
  text: "",
  startTime: 0,
  maxResults: 1
}).then(onGot);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/deleteUrl

### deleteRange()
Removes all visits to pages that the user made during the given time range.

**Syntax**: `browser.history.deleteRange(range)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `range` | object | Yes | - | Time range specification |
| `range.startTime` | number/string/Date | Yes | - | Start time for the range |
| `range.endTime` | number/string/Date | Yes | - | End time for the range |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the range has been deleted

#### Code Examples
```javascript
const MINUTE = 60 * 1000;

function oneMinuteAgo() {
  return Date.now() - MINUTE;
}

browser.history.deleteRange({
  startTime: oneMinuteAgo(),
  endTime: Date.now()
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/deleteRange

### deleteAll()
Deletes all visits from the browser's history. Triggers `history.onVisitRemoved` once with `allHistory` set to true.

**Syntax**: `browser.history.deleteAll()`

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when all history has been deleted

#### Code Examples
```javascript
function onDeleteAll() {
  console.log("Deleted all history");
}

function deleteAllHistory() {
  let deletingAll = browser.history.deleteAll();
  deletingAll.then(onDeleteAll);
}

deleteAllHistory();
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/deleteAll

## Events

### onTitleChanged
Fired when the title of a page visited by the user is recorded.

**Note**: `history.onVisited` fires before page loads, so title isn't known yet. This event fires after the page loads when the title becomes available.

**Syntax**: `browser.history.onTitleChanged.addListener(listener)`

**Listener receives**:
- `object` with properties:
  - `id` (string): The unique identifier for the HistoryItem
  - `url` (string): URL of the page
  - `title` (string): New title of the page

### onVisited
Fired each time the user visits a page. Fires before the page has loaded.

**Syntax**: `browser.history.onVisited.addListener(listener)`

**Listener receives**:
- `HistoryItem`: The history item for the visited page

**Note**: At the time this event is sent, the browser doesn't yet know the page title. If the browser has visited this page before and remembered its old title, then `HistoryItem.title` will contain the old title. Otherwise it will be empty.

#### Code Examples
```javascript
function onVisited(historyItem) {
  console.log(historyItem.url);
  console.log(new Date(historyItem.lastVisitTime));
}

browser.history.onVisited.addListener(onVisited);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/onVisited

### onVisitRemoved
Fired when a URL is removed completely from the browser history.

**Syntax**: `browser.history.onVisitRemoved.addListener(listener)`

**Listener receives**:
- `removed` (object):
  - `allHistory` (boolean): `true` if all history was cleared
  - `urls` (array): Array of removed URLs (empty if `allHistory` is true)

**Behavior**:
- Single page removal: Fired once
- Range removal: Fired once for each page whose visits all fall within the range
- All history cleared: Fired only once with `allHistory: true`

#### Code Examples
```javascript
function onRemoved(removed) {
  if (removed.allHistory) {
    console.log("All history removed");
  } else if (removed.urls.length) {
    console.log(`URL removed: ${removed.urls[0]}`);
  }
}

browser.history.onVisitRemoved.addListener(onRemoved);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/history/onVisitRemoved

## Related APIs
- `bookmarks` - Manage browser bookmarks
- `downloads` - Interact with download manager
- `tabs` - Access and manipulate browser tabs