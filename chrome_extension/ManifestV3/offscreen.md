---
title: chrome.offscreen
url: https://developer.chrome.com/docs/extensions/reference/api/offscreen
---

# `chrome.offscreen`

## Description

Use the `offscreen` API to create and manage offscreen documents.

## Permissions

`offscreen`

To use the Offscreen API, declare the "offscreen" permission in the extension manifest. For example:

```
{ "name": "My extension", ... "permissions": [ "offscreen" ], ... }
```

## Availability

Chrome 109+ MV3+

## Concepts and usage

Service workers don't have DOM access, and many websites have content security policies that limit the functionality of content scripts. The Offscreen API allows the extension to use DOM APIs in a hidden document without interrupting the user experience by opening new windows or tabs. The `runtime` API is the only extensions API supported by offscreen documents.

Pages loaded as offscreen documents are handled differently from other types of extension pages. The extension's permissions carry over to offscreen documents, but with limits on extension API access. For example, because the `chrome.runtime` API is the only extensions API supported by offscreen documents, messaging must be handled using members of that API.

The following are other ways offscreen documents behave differently from normal pages:

*   An offscreen document's URL must be a static HTML file bundled with the extension.
*   Offscreen documents can't be focused.
*   An offscreen document is an instance of `window`, but the value of its `opener` property is always null.
*   Though an extension package can contain multiple offscreen documents, an installed extension can only have one open at a time. If the extension is running in split mode with an active incognito profile, the normal and incognito profiles can each have one offscreen document.

Use `chrome.offscreen.createDocument()` and `chrome.offscreen.closeDocument()` to create and close an offscreen document. `createDocument()` requires the document's url, a reason, and a justification:

```
chrome.offscreen.createDocument({ url: 'off_screen.html', reasons: ['CLIPBOARD'], justification: 'reason for needing the document', });
```

### Reasons

For a list of valid reasons, see the Reasons section. Reasons are set during document creation to determine the document's lifespan. The `AUDIO_PLAYBACK` reason sets the document to close after 30 seconds without audio playing. All other reasons don't set lifetime limits.

## Examples

### Maintain the lifecycle of an offscreen document

The following example shows how to ensure that an offscreen document exists. The `setupOffscreenDocument()` function calls `runtime.getContexts()` to find an existing offscreen document, or creates the document if it doesn't already exist.

```
let creating; // A global promise to avoid concurrency issues async function setupOffscreenDocument(path) { // Check all windows controlled by the service worker to see if one // of them is the offscreen document with the given path const offscreenUrl = chrome.runtime.getURL(path); const existingContexts = await chrome.runtime.getContexts({ contextTypes: ['OFFSCREEN_DOCUMENT'], documentUrls: [offscreenUrl] }); if (existingContexts.length > 0) { return; } // create offscreen document if (creating) { await creating; } else { creating = chrome.offscreen.createDocument({ url: path, reasons: ['CLIPBOARD'], justification: 'reason for needing the document', }); await creating; creating = null; } }
```

Before sending a message to an offscreen document, call `setupOffscreenDocument()` to make sure the document exists, as demonstrated in the following example.

```
chrome.action.onClicked.addListener(async () => { await setupOffscreenDocument('off_screen.html'); // Send message to offscreen document chrome.runtime.sendMessage({ type: '...', target: 'offscreen', data: '...' }); });
```

For complete examples, see the [offscreen-clipboard](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api-samples/offscreen-clipboard) and [offscreen-dom](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api-samples/offscreen-dom) demos on GitHub.

### Before Chrome 116: check if an offscreen document is open

`runtime.getContexts()` was added in Chrome 116. In earlier versions of Chrome, use `clients.matchAll()` to check for an existing offscreen document:

```
async function hasOffscreenDocument() { if ('getContexts' in chrome.runtime) { const contexts = await chrome.runtime.getContexts({ contextTypes: ['OFFSCREEN_DOCUMENT'], documentUrls: [OFFSCREEN_DOCUMENT_PATH] }); return Boolean(contexts.length); } else { const matchedClients = await clients.matchAll(); return matchedClients.some(client => { return client.url.includes(chrome.runtime.id); }); } }
```

## Types

### `CreateParameters`

#### Properties

*   `justification`: `string`

    A developer-provided string that explains, in more detail, the need for the background context. The user agent \_may\_ use this in display to the user.
*   `reasons`: `Reason[]`

    The reason(s) the extension is creating the offscreen document.
*   `url`: `string`

    The (relative) URL to load in the document.

### `Reason`

#### Enum

*   `"TESTING"`: A reason used for testing purposes only.
*   `"AUDIO_PLAYBACK"`: Specifies that the offscreen document is responsible for playing audio.
*   `"IFRAME_SCRIPTING"`: Specifies that the offscreen document needs to embed and script an iframe in order to modify the iframe's content.
*   `"DOM_SCRAPING"`: Specifies that the offscreen document needs to embed an iframe and scrape its DOM to extract information.
*   `"BLOBS"`: Specifies that the offscreen document needs to interact with `Blob` objects (including `URL.createObjectURL()`).
*   `"DOM_PARSER"`: Specifies that the offscreen document needs to use the `DOMParser` API.
*   `"USER_MEDIA"`: Specifies that the offscreen document needs to interact with media streams from user media (e.g. `getUserMedia()`).
*   `"DISPLAY_MEDIA"`: Specifies that the offscreen document needs to interact with media streams from display media (e.g. `getDisplayMedia()`).
*   `"WEB_RTC"`: Specifies that the offscreen document needs to use WebRTC APIs.
*   `"CLIPBOARD"`: Specifies that the offscreen document needs to interact with the Clipboard API.
*   `"LOCAL_STORAGE"`: Specifies that the offscreen document needs access to `localStorage`.
*   `"WORKERS"`: Specifies that the offscreen document needs to spawn workers.
*   `"BATTERY_STATUS"`: Specifies that the offscreen document needs to use `navigator.getBattery`.
*   `"MATCH_MEDIA"`: Specifies that the offscreen document needs to use `window.matchMedia`.
*   `"GEOLOCATION"`: Specifies that the offscreen document needs to use `navigator.geolocation`.

## Methods

### `closeDocument()`

`Promise`

```
chrome.offscreen.closeDocument( callback?: function, )
```

Closes the currently-open offscreen document for the extension.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `createDocument()`

`Promise`

```
chrome.offscreen.createDocument( parameters: CreateParameters, callback?: function, )
```

Creates a new offscreen document for the extension.

#### Parameters

*   `parameters`: `CreateParameters`

    The parameters describing the offscreen document to create.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 