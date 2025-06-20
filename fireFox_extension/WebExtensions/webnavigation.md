# WebNavigation

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webNavigation
- **Version**: Firefox WebExtensions API

## Overview

Add event listeners for the various stages of a navigation. A navigation consists of a frame in the browser transitioning from one URL to another, usually (but not always) in response to a user action like clicking a link or entering a URL in the location bar.

Compared with the webRequest API: navigations usually result in the browser making web requests, but the webRequest API is concerned with the lower-level view from the HTTP layer, while the webNavigation API is more concerned with the view from the browser UI itself.

## Permissions
- `"webNavigation"` - Required to use this API

## Navigation Flow

### Primary Event Sequence
1. `onBeforeNavigate` - Browser is about to start navigation
2. `onCommitted` - Navigation is committed, document starts loading
3. `onDOMContentLoaded` - DOM content loaded (equivalent to DOMContentLoaded event)
4. `onCompleted` - Document and resources completely loaded

### Additional Events
- `onCreatedNavigationTarget` - Fired before onBeforeNavigate if new tab/window created
- `onHistoryStateUpdated` - Fired when page uses History API to update URL
- `onReferenceFragmentUpdated` - Fired when fragment identifier changes
- `onErrorOccurred` - Fired when navigation error occurs (can happen at any point)
- `onTabReplaced` - Fired when tab contents replaced by different tab

## Types

### TransitionType
| Value | Description |
|-------|-------------|
| `"link"` | User clicked a link |
| `"typed"` | User typed URL in address bar |
| `"auto_bookmark"` | User clicked bookmark |
| `"auto_subframe"` | Subframe navigation |
| `"manual_subframe"` | Manual subframe navigation |
| `"generated"` | User submitted form |
| `"start_page"` | Start page |
| `"form_submit"` | Form submission |
| `"reload"` | Page reload |
| `"keyword"` | URL generated from keyword |
| `"keyword_generated"` | Keyword-generated navigation |

### TransitionQualifier
Array of strings providing extra information about transition:
- `"client_redirect"` - Redirected by JavaScript or meta refresh
- `"server_redirect"` - Redirected by HTTP redirect response
- `"forward_back"` - User used forward/back button
- `"from_address_bar"` - User typed in address bar

## Methods

### getFrame()
**Syntax**: `webNavigation.getFrame(details)`

Retrieves information about a particular frame.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| details | object | Yes | Frame identification details |
| details.tabId | integer | Yes | ID of the tab |
| details.frameId | integer | Yes | ID of the frame |
| details.processId | integer | No | Process ID (Edge specific) |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Frame information object

#### Frame Info Properties
| Property | Type | Description |
|----------|------|-------------|
| errorOccurred | boolean | True if last navigation was interrupted by error |
| url | string | URL currently associated with frame |
| parentFrameId | integer | ID of parent frame (-1 for top-level) |

#### Code Examples
```javascript
function onGot(frameInfo) {
  console.log(frameInfo);
}

function onError(error) {
  console.log(`Error: ${error}`);
}

let gettingFrame = browser.webNavigation.getFrame({
  tabId: 19,
  frameId: 1537,
});

gettingFrame.then(onGot, onError);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webNavigation/getFrame

### getAllFrames()
**Syntax**: `webNavigation.getAllFrames(details)`

Given a tab ID, retrieves information about all frames it contains.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| details | object | Yes | Tab identification |
| details.tabId | integer | Yes | ID of the tab |

#### Returns
- **Type**: `Promise<array>`
- **Description**: Array of frame information objects

#### Code Examples
```javascript
function logFrameInfo(framesInfo) {
  for (const frameInfo of framesInfo) {
    console.log(frameInfo);
  }
}

function onError(error) {
  console.error(`Error: ${error}`);
}

function logAllFrames(tabs) {
  browser.webNavigation
    .getAllFrames({
      tabId: tabs[0].id,
    })
    .then(logFrameInfo, onError);
}

browser.browserAction.onClicked.addListener(() => {
  browser.tabs
    .query({
      currentWindow: true,
      active: true,
    })
    .then(logAllFrames, onError);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webNavigation/getAllFrames

## Events

### onBeforeNavigate
**Fired when**: Browser is about to start a navigation event

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Target URL |
| frameId | integer | Frame ID (0 for main frame) |
| parentFrameId | integer | Parent frame ID (-1 for main frame) |
| timeStamp | number | Time when navigation was about to start |

#### Code Examples
```javascript
browser.webNavigation.onBeforeNavigate.addListener((details) => {
  console.log("About to navigate to:", details.url);
});

// With URL filter
const filter = {
  url: [
    {hostContains: "example.com"},
    {hostPrefix: "developer"}
  ]
};

browser.webNavigation.onBeforeNavigate.addListener(
  (details) => {
    console.log("Filtered navigation:", details.url);
  },
  filter
);
```

### onCommitted
**Fired when**: Navigation is committed, document starts loading

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Target URL |
| frameId | integer | Frame ID |
| transitionType | TransitionType | Cause of navigation |
| transitionQualifiers | TransitionQualifier[] | Additional transition info |
| timeStamp | number | Time when navigation was committed |

#### Code Examples
```javascript
const filter = {
  url: [
    {hostContains: "example.com"},
    {hostPrefix: "developer"}
  ]
};

function logOnCommitted(details) {
  console.log("target URL: " + details.url);
  console.log("transition type: " + details.transitionType);
  console.log("transition qualifiers: " + details.transitionQualifiers);
}

browser.webNavigation.onCommitted.addListener(logOnCommitted, filter);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webNavigation

### onDOMContentLoaded
**Fired when**: DOMContentLoaded event fires in the page

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Document URL |
| frameId | integer | Frame ID |
| timeStamp | number | Time when DOMContentLoaded fired |

### onCompleted
**Fired when**: Document and all resources completely loaded

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Document URL |
| frameId | integer | Frame ID |
| timeStamp | number | Time when loading completed |

### onErrorOccurred
**Fired when**: Navigation error occurs

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Target URL |
| frameId | integer | Frame ID |
| error | string | Error description |
| timeStamp | number | Time when error occurred |

### onCreatedNavigationTarget
**Fired when**: New window/tab created for navigation

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| sourceTabId | integer | Source tab ID |
| sourceFrameId | integer | Source frame ID |
| url | string | Target URL |
| tabId | integer | New tab ID |
| timeStamp | number | Time when target was created |

### onReferenceFragmentUpdated
**Fired when**: Fragment identifier for page changes

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Updated URL |
| frameId | integer | Frame ID |
| transitionType | TransitionType | Transition type |
| transitionQualifiers | TransitionQualifier[] | Transition qualifiers |
| timeStamp | number | Time of fragment update |

#### Code Examples
```javascript
const filter = {
  url: [
    {hostContains: "example.com"},
    {hostPrefix: "developer"}
  ]
};

function logOnReferenceFragmentUpdated(details) {
  console.log("onReferenceFragmentUpdated: " + details.url);
  console.log("Transition type: " + details.transitionType);
  console.log("Transition qualifiers: " + details.transitionQualifiers);
}

browser.webNavigation.onReferenceFragmentUpdated.addListener(
  logOnReferenceFragmentUpdated, 
  filter
);
```

### onHistoryStateUpdated
**Fired when**: Page uses History API to update URL

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| tabId | integer | ID of the tab |
| url | string | Updated URL |
| frameId | integer | Frame ID |
| transitionType | TransitionType | Transition type |
| transitionQualifiers | TransitionQualifier[] | Transition qualifiers |
| timeStamp | number | Time of history update |

### onTabReplaced
**Fired when**: Tab contents replaced by different tab

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| replacedTabId | integer | ID of replaced tab |
| tabId | integer | ID of replacement tab |
| timeStamp | number | Time of replacement |

## Frame Navigation

Each navigation occurs in a browser frame identified by:
- **Tab ID**: Identifies the browser tab
- **Frame ID**: Identifies the frame within the tab
  - `0` indicates the main (top-level) frame
  - Positive values indicate subframes (iframes)

### Subframe Behavior
- Parent frame's `onCommitted` fires before children's `onBeforeNavigate`
- Parent frame's `onCompleted` fires after all children's `onCompleted`
- Frame IDs are unique within a tab and process

## URL Filtering

All events support optional URL filtering:

```javascript
const filter = {
  url: [
    {hostContains: "example.com"},
    {hostPrefix: "developer"},
    {hostSuffix: ".org"},
    {pathPrefix: "/api/"},
    {schemes: ["https"]}
  ]
};

browser.webNavigation.onCommitted.addListener(listener, filter);
```

## Related APIs
- `webRequest` - HTTP-level request monitoring
- `tabs` - Tab management and information
- `history` - Browser history access

## Notes
- Based on Chromium's chrome.webNavigation API
- TimeStamp values are internally consistent for comparison
- Pre-rendered tabs become accessible after onTabReplaced event
- Some navigations may not correspond to visible tabs in browser UI
