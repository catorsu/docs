# Extension

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extension
- **Version**: All versions

## Overview
Utilities related to your extension. Get URLs to resources packaged with your extension. Get the Window object for your extension's pages. Get the values for various settings.

Note: The messaging APIs in this module are deprecated in favor of the equivalent APIs in the runtime module.

## Permissions
- No special permissions required

## Types
### ViewType
| Value | Description |
|-------|-------------|
| "tab" | Views in tabs |
| "popup" | Popup windows such as action popups |
| "sidebar" | Sidebar views |

## Properties
### lastError (Deprecated)
**Type**: `object` or `undefined`
**Description**: Set for the lifetime of a callback if an asynchronous extension API has resulted in an error. If no error has occurred, lastError will be undefined.

### inIncognitoContext
**Type**: `boolean`
**Description**: True for content scripts running inside incognito tabs, and for extension pages running inside an incognito process. (The latter only applies to extensions with "incognito": "split" set in their manifest.json file.)

## Methods
### getBackgroundPage()
**Syntax**: `browser.extension.getBackgroundPage()`

Returns the Window object for the background page running inside the current extension. Returns null if the extension has no background page.

#### Parameters
None

#### Returns
- **Type**: `Window` or `null`
- **Description**: The Window object for the background page, or null

#### Code Examples
```javascript
const backgroundPage = browser.extension.getBackgroundPage();
if (backgroundPage) {
  // Call a function in the background page
  backgroundPage.doSomething();
}
```

### getExtensionTabs() (Deprecated)
**Syntax**: `browser.extension.getExtensionTabs()`

Returns an array of the JavaScript Window objects for each of the tabs running inside the current extension.

#### Parameters
None

#### Returns
- **Type**: `Array<Window>`
- **Description**: Array of Window objects

#### Code Examples
No code examples in source documentation

### getURL() (Deprecated)
**Syntax**: `browser.extension.getURL(path)`

Converts a relative path within an extension install directory to a fully-qualified URL.

Note: Use runtime.getURL() instead.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| path | string | Yes | - | A path relative to the extension root |

#### Returns
- **Type**: `string`
- **Description**: The fully-qualified URL

#### Code Examples
```javascript
const url = browser.extension.getURL("images/icon.png");
// Returns something like: "moz-extension://[extension-id]/images/icon.png"
```

### getViews()
**Syntax**: `browser.extension.getViews(fetchProperties)`

Returns an array of the Window objects for each of the pages running inside the current extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| fetchProperties | object | No | {} | Properties to filter views |
| fetchProperties.type | ViewType | No | - | The type of view to get |
| fetchProperties.windowId | integer | No | - | The window to restrict the search to |

#### Returns
- **Type**: `Array<Window>`
- **Description**: Array of Window objects matching the criteria

#### Code Examples
```javascript
// Get all windows
const windows = browser.extension.getViews();
for (const extensionWindow of windows) {
  console.log(extensionWindow.location.href);
}

// Get only windows in browser tabs
const tabWindows = browser.extension.getViews({type: "tab"});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extension/getViews

### isAllowedIncognitoAccess()
**Syntax**: `browser.extension.isAllowedIncognitoAccess()`

Retrieves the state of the extension's access to Incognito-mode (as determined by the user-controlled 'Allowed in Incognito' checkbox).

#### Parameters
None

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the extension has access to Incognito mode

#### Code Examples
```javascript
browser.extension.isAllowedIncognitoAccess().then((allowed) => {
  if (allowed) {
    console.log("Extension can run in incognito mode");
  }
});
```

### isAllowedFileSchemeAccess()
**Syntax**: `browser.extension.isAllowedFileSchemeAccess()`

Retrieves the state of the extension's access to the file:// scheme (as determined by the user-controlled 'Allow access to File URLs' checkbox).

#### Parameters
None

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the extension can access file:// URLs

#### Code Examples
```javascript
browser.extension.isAllowedFileSchemeAccess().then((allowed) => {
  if (allowed) {
    console.log("Extension can access file URLs");
  }
});
```

### sendRequest() (Deprecated)
**Syntax**: `browser.extension.sendRequest(extensionId, request)`

Sends a single request to other listeners within the extension.

Note: Use runtime.sendMessage() instead.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| extensionId | string | No | - | The extension ID to send to |
| request | any | Yes | - | The request to send |

#### Returns
- **Type**: `Promise<any>`
- **Description**: The response from the handler

#### Code Examples
No code examples in source documentation

### setUpdateUrlData()
**Syntax**: `browser.extension.setUpdateUrlData(data)`

Sets the value of the ap CGI parameter used in the extension's update URL. This value is ignored for extensions that are hosted in the browser vendor's store.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| data | string | Yes | - | The data to include in update pings |

#### Returns
None

#### Code Examples
No code examples in source documentation

## Events
### onRequest (Deprecated)
**Fired when**: A request is sent from either an extension process or a content script

Note: Use runtime.onMessage instead.

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| request | any | The request sent by the calling script |
| sender | runtime.MessageSender | An object containing information about the script context that sent the request |
| sendResponse | function | Function to call when you have a response |

### onRequestExternal (Deprecated)
**Fired when**: A request is sent from another extension

Note: Use runtime.onMessageExternal instead.

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| request | any | The request sent by the calling script |
| sender | runtime.MessageSender | An object containing information about the script context that sent the request |
| sendResponse | function | Function to call when you have a response |

## Related APIs
- `runtime` - The modern API for extension utilities and messaging
- `management` - For managing extensions
- `tabs` - For working with browser tabs