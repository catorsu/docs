---
title: chrome.windows
url: https://developer.chrome.com/docs/extensions/reference/api/windows
---

## Description

Use the `chrome.windows` API to interact with browser windows. You can use this API to create, modify, and rearrange windows in the browser.

## Permissions

When requested, a `windows.Window` contains an array of `tabs.Tab` objects. You must declare the `"tabs"` permission in your manifest if you need access to the `url`, `pendingUrl`, `title`, or `favIconUrl` properties of `tabs.Tab`. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": ["tabs"],
  ...
}
```

## Concepts and usage

### The current window

Many functions in the extension system take an optional `windowId` argument, which defaults to the current window.

The current window is the window that contains the code that is currently executing. It's important to realize that this can be different from the topmost or focused window.

For example, say an extension creates a few tabs or windows from a single HTML file, and that the HTML file contains a call to `tabs.query()`. The current window is the window that contains the page that made the call, no matter what the topmost window is.

In the case of service workers, the value of the current window falls back to the last active window. Under some circumstances, there may be no current window for background pages.

## Examples

To try this API, install the windows API example from the [chrome-extension-samples](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api/windows) repository.

Two windows, each with one tab.

## Types

### CreateType

Chrome 44+

Specifies what type of browser window to create. `'panel'` is deprecated and is available only to existing allowlisted extensions on Chrome OS.

#### Enum

*   `"normal"`: Specifies the window as a standard window.
*   `"popup"`: Specifies the window as a popup window.
*   `"panel"`: Specifies the window as a panel.

### QueryOptions

Chrome 88+

#### Properties

*   `populate`
    *   `boolean` optional
    *   If `true`, the `windows.Window` object has a `tabs` property that contains a list of the `tabs.Tab` objects. The `Tab` objects only contain the `url`, `pendingUrl`, `title`, and `favIconUrl` properties if the extension's manifest file includes the `"tabs"` permission.
*   `windowTypes`
    *   `WindowType[]` optional
    *   If set, the `windows.Window` returned is filtered based on its type. If unset, the default filter is set to `['normal', 'popup']`.

### Window

#### Properties

*   `alwaysOnTop`
    *   `boolean`
    *   Whether the window is set to be always on top.
*   `focused`
    *   `boolean`
    *   Whether the window is currently the focused window.
*   `height`
    *   `number` optional
    *   The height of the window, including the frame, in pixels. In some circumstances a window may not be assigned a `height` property; for example, when querying closed windows from the `sessions` API.
*   `id`
    *   `number` optional
    *   The ID of the window. Window IDs are unique within a browser session. In some circumstances a window may not be assigned an `ID` property; for example, when querying windows using the `sessions` API, in which case a session ID may be present.
*   `incognito`
    *   `boolean`
    *   Whether the window is incognito.
*   `left`
    *   `number` optional
    *   The offset of the window from the left edge of the screen in pixels. In some circumstances a window may not be assigned a `left` property; for example, when querying closed windows from the `sessions` API.
*   `sessionId`
    *   `string` optional
    *   The session ID used to uniquely identify a window, obtained from the `sessions` API.
*   `state`
    *   `WindowState` optional
    *   The state of this browser window.
*   `tabs`
    *   `Tab[]` optional
    *   Array of `tabs.Tab` objects representing the current tabs in the window.
*   `top`
    *   `number` optional
    *   The offset of the window from the top edge of the screen in pixels. In some circumstances a window may not be assigned a `top` property; for example, when querying closed windows from the `sessions` API.
*   `type`
    *   `WindowType` optional
    *   The type of browser window this is.
*   `width`
    *   `number` optional
    *   The width of the window, including the frame, in pixels. In some circumstances a window may not be assigned a `width` property; for example, when querying closed windows from the `sessions` API.

### WindowState

Chrome 44+

The state of this browser window. In some circumstances a window may not be assigned a `state` property; for example, when querying closed windows from the `sessions` API.

#### Enum

*   `"normal"`: Normal window state (not minimized, maximized, or fullscreen).
*   `"minimized"`: Minimized window state.
*   `"maximized"`: Maximized window state.
*   `"fullscreen"`: Fullscreen window state.
*   `"locked-fullscreen"`: Locked fullscreen window state. This fullscreen state cannot be exited by user action and is available only to allowlisted extensions on Chrome OS.

### WindowType

Chrome 44+

The type of browser window this is. In some circumstances a window may not be assigned a `type` property; for example, when querying closed windows from the `sessions` API.

#### Enum

*   `"normal"`: A normal browser window.
*   `"popup"`: A browser popup.
*   `"panel"`: Deprecated in this API. A Chrome App panel-style window. Extensions can only see their own panel windows.
*   `"app"`: Deprecated in this API. A Chrome App window. Extensions can only see their app own windows.
*   `"devtools"`: A Developer Tools window.

## Properties

### WINDOW_ID_CURRENT

The `windowId` value that represents the current window.

#### Value

`-2`

### WINDOW_ID_NONE

The `windowId` value that represents the absence of a Chrome browser window.

#### Value

`-1`

## Methods

### create()

`Promise`

```javascript
chrome.windows.create(
  createData?: object,
  callback?: function,
)
```

Creates (opens) a new browser window with any optional sizing, position, or default URL provided.

#### Parameters

*   `createData`
    *   `object` optional
    *   `focused`
        *   `boolean` optional
        *   If `true`, opens an active window. If `false`, opens an inactive window.
    *   `height`
        *   `number` optional
        *   The height in pixels of the new window, including the frame. If not specified, defaults to a natural height.
    *   `incognito`
        *   `boolean` optional
        *   Whether the new window should be an incognito window.
    *   `left`
        *   `number` optional
        *   The number of pixels to position the new window from the left edge of the screen. If not specified, the new window is offset naturally from the last focused window. This value is ignored for panels.
    *   `setSelfAsOpener`
        *   `boolean` optional
        *   Chrome 64+
        *   If `true`, the newly-created window's `'window.opener'` is set to the caller and is in the same unit of related browsing contexts as the caller.
    *   `state`
        *   `WindowState` optional
        *   Chrome 44+
        *   The initial state of the window. The `minimized`, `maximized`, and `fullscreen` states cannot be combined with `left`, `top`, `width`, or `height`.
    *   `tabId`
        *   `number` optional
        *   The ID of the tab to add to the new window.
    *   `top`
        *   `number` optional
        *   The number of pixels to position the new window from the top edge of the screen. If not specified, the new window is offset naturally from the last focused window. This value is ignored for panels.
    *   `type`
        *   `CreateType` optional
        *   Specifies what type of browser window to create.
    *   `url`
        *   `string | string[]` optional
        *   A URL or array of URLs to open as tabs in the window. Fully-qualified URLs must include a scheme, e.g., `'http://www.google.com'`, not `'www.google.com'`. Non-fully-qualified URLs are considered relative within the extension. Defaults to the New Tab Page.
    *   `width`
        *   `number` optional
        *   The width in pixels of the new window, including the frame. If not specified, defaults to a natural width.
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (window?: Window) => void
        ```
    *   `window`
        *   `Window` optional
        *   Contains details about the created window.

#### Returns

*   `Promise<Window | undefined>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### get()

`Promise`

```javascript
chrome.windows.get(
  windowId: number,
  queryOptions?: QueryOptions,
  callback?: function,
)
```

Gets details about a window.

#### Parameters

*   `windowId`
    *   `number`
*   `queryOptions`
    *   `QueryOptions` optional
    *   Chrome 88+
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`

#### Returns

*   `Promise<Window>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAll()

`Promise`

```javascript
chrome.windows.getAll(
  queryOptions?: QueryOptions,
  callback?: function,
)
```

Gets all windows.

#### Parameters

*   `queryOptions`
    *   `QueryOptions` optional
    *   Chrome 88+
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (windows: Window[]) => void
        ```
    *   `windows`
        *   `Window[]`

#### Returns

*   `Promise<Window[]>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getCurrent()

`Promise`

```javascript
chrome.windows.getCurrent(
  queryOptions?: QueryOptions,
  callback?: function,
)
```

Gets the current window.

#### Parameters

*   `queryOptions`
    *   `QueryOptions` optional
    *   Chrome 88+
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`

#### Returns

*   `Promise<Window>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getLastFocused()

`Promise`

```javascript
chrome.windows.getLastFocused(
  queryOptions?: QueryOptions,
  callback?: function,
)
```

Gets the window that was most recently focused — typically the window 'on top'.

#### Parameters

*   `queryOptions`
    *   `QueryOptions` optional
    *   Chrome 88+
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`

#### Returns

*   `Promise<Window>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### remove()

`Promise`

```javascript
chrome.windows.remove(
  windowId: number,
  callback?: function,
)
```

Removes (closes) a window and all the tabs inside it.

#### Parameters

*   `windowId`
    *   `number`
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        () => void
        ```

#### Returns

*   `Promise<void>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### update()

`Promise`

```javascript
chrome.windows.update(
  windowId: number,
  updateInfo: object,
  callback?: function,
)
```

Updates the properties of a window. Specify only the properties that to be changed; unspecified properties are unchanged.

#### Parameters

*   `windowId`
    *   `number`
*   `updateInfo`
    *   `object`
    *   `drawAttention`
        *   `boolean` optional
        *   If `true`, causes the window to be displayed in a manner that draws the user's attention to the window, without changing the focused window. The effect lasts until the user changes focus to the window. This option has no effect if the window already has focus. Set to `false` to cancel a previous `drawAttention` request.
    *   `focused`
        *   `boolean` optional
        *   If `true`, brings the window to the front; cannot be combined with the `state 'minimized'`. If `false`, brings the next window in the z-order to the front; cannot be combined with the `state 'fullscreen'` or `'maximized'`.
    *   `height`
        *   `number` optional
        *   The height to resize the window to in pixels. This value is ignored for panels.
    *   `left`
        *   `number` optional
        *   The offset from the left edge of the screen to move the window to in pixels. This value is ignored for panels.
    *   `state`
        *   `WindowState` optional
        *   The new state of the window. The `'minimized'`, `'maximized'`, and `'fullscreen'` states cannot be combined with `'left'`, `'top'`, `'width'`, or `'height'`.
    *   `top`
        *   `number` optional
        *   The offset from the top edge of the screen to move the window to in pixels. This value is ignored for panels.
    *   `width`
        *   `number` optional
        *   The width to resize the window to in pixels. This value is ignored for panels.
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`

#### Returns

*   `Promise<Window>`
    *   Chrome 88+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onBoundsChanged

Chrome 86+

```javascript
chrome.windows.onBoundsChanged.addListener(
  callback: function,
)
```

Fired when a window has been resized; this event is only dispatched when the new bounds are committed, and not for in-progress changes.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`

### onCreated

```javascript
chrome.windows.onCreated.addListener(
  callback: function,
  filters?: object,
)
```

Fired when a window is created.

#### Parameters

*   `callback`
    *   `function`
    *   Chrome 46+
    *   The callback parameter looks like:
        ```javascript
        (window: Window) => void
        ```
    *   `window`
        *   `Window`
        *   Details of the created window.
*   `filters`
    *   `object` optional
    *   `windowTypes`
        *   `WindowType[]`
        *   Conditions that the window's type being created must satisfy. By default it satisfies `['normal', 'popup']`.

### onFocusChanged

```javascript
chrome.windows.onFocusChanged.addListener(
  callback: function,
  filters?: object,
)
```

Fired when the currently focused window changes. Returns `chrome.windows.WINDOW_ID_NONE` if all Chrome windows have lost focus. Note: On some Linux window managers, `WINDOW_ID_NONE` is always sent immediately preceding a switch from one Chrome window to another.

#### Parameters

*   `callback`
    *   `function`
    *   Chrome 46+
    *   The callback parameter looks like:
        ```javascript
        (windowId: number) => void
        ```
    *   `windowId`
        *   `number`
        *   ID of the newly-focused window.
*   `filters`
    *   `object` optional
    *   `windowTypes`
        *   `WindowType[]`
        *   Conditions that the window's type being removed must satisfy. By default it satisfies `['normal', 'popup']`.

### onRemoved

```javascript
chrome.windows.onRemoved.addListener(
  callback: function,
  filters?: object,
)
```

Fired when a window is removed (closed).

#### Parameters

*   `callback`
    *   `function`
    *   Chrome 46+
    *   The callback parameter looks like:
        ```javascript
        (windowId: number) => void
        ```
    *   `windowId`
        *   `number`
        *   ID of the removed window.
*   `filters`
    *   `object` optional
    *   `windowTypes`
        *   `WindowType[]`
        *   Conditions that the window's type being removed must satisfy. By default it satisfies `['normal', 'popup']`. 