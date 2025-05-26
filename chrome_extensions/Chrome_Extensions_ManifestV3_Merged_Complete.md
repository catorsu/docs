<chrome-api>
---
title: chrome.accessibilityFeatures
url: https://developer.chrome.com/docs/extensions/reference/api/accessibilityFeatures
---

# chrome.accessibilityFeatures Stay organized with collections Save and categorize content based on your preferences.

## Description

Use the `chrome.accessibilityFeatures` API to manage Chrome's accessibility features. This API relies on the `ChromeSetting` prototype of the `type` API for getting and setting individual accessibility features. In order to get feature states the extension must request `accessibilityFeatures.read` permission. For modifying feature state, the extension needs `accessibilityFeatures.modify` permission. Note that `accessibilityFeatures.modify` does not imply `accessibilityFeatures.read` permission.

## Permissions

`accessibilityFeatures.modify` `accessibilityFeatures.read`

## Properties

### animationPolicy

`get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<"allowed" | "once" | "none" >`

### autoclick

ChromeOS only.

Auto mouse click after mouse stops moving. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### caretHighlight

Chrome 51+

ChromeOS only.

Caret highlighting. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### cursorColor

Chrome 85+

ChromeOS only.

Cursor color. The value indicates whether the feature is enabled or not, doesn't indicate the color of it. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### cursorHighlight

Chrome 51+

ChromeOS only.

Cursor highlighting. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### dictation

Chrome 90+

ChromeOS only.

Dictation. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### dockedMagnifier

Chrome 87+

ChromeOS only.

Docked magnifier. The value indicates whether docked magnifier feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### focusHighlight

Chrome 51+

ChromeOS only.

Focus highlighting. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### highContrast

ChromeOS only.

High contrast rendering mode. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### largeCursor

ChromeOS only.

Enlarged cursor. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### screenMagnifier

ChromeOS only.

Full screen magnification. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### selectToSpeak

Chrome 51+

ChromeOS only.

Select-to-speak. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### spokenFeedback

ChromeOS only.

Spoken feedback (text-to-speech). The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### stickyKeys

ChromeOS only.

Sticky modifier keys (like shift or alt). The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### switchAccess

Chrome 51+

ChromeOS only.

Switch Access. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

### virtualKeyboard

ChromeOS only.

Virtual on-screen keyboard. The value indicates whether the feature is enabled or not. `get()` requires `accessibilityFeatures.read` permission. `set()` and `clear()` require `accessibilityFeatures.modify` permission.

#### Type

`types.ChromeSetting<boolean>`

===

---
title: chrome.action
url: https://developer.chrome.com/docs/extensions/reference/api/action
---

# chrome.action

## Description

Use the `chrome.action` API to control the extension's icon in the Google Chrome toolbar.

The action icons are displayed in the browser toolbar next to the omnibox. After installation, these appear in the extensions menu (the puzzle piece icon). Users can pin your extension icon to the toolbar.

## Availability

Chrome 88+ MV3+

## Manifest

The following keys must be declared in the manifest to use this API.

`"action"`

To use the `chrome.action` API, specify a `manifest_version` of 3 and include the `"action"` key in your manifest file.

Note: Every extension has an icon in the Chrome toolbar, even if the `"action"` key isn't added to the manifest.

```json
{
  "name": "Action Extension",
  ...
  "action": {
    "default_icon": { // optional
      "16": "images/icon16.png", // optional
      "24": "images/icon24.png", // optional
      "32": "images/icon32.png"  // optional
    },
    "default_title": "Click Me", // optional, shown in tooltip
    "default_popup": "popup.html" // optional
  },
  ...
}
```

The `"action"` key (along with its children) is optional. When it isn't included, your extension is still shown in the toolbar to provide access to the extension's menu. For this reason, we recommend that you always include at least the `"action"` and `"default_icon"` keys.

## Concepts and usage

### Icon

The icon is the main image on the toolbar for your extension, and is set by the `"default_icon"` key in your manifest's `"action"` key. Icons must be 16 device-independent pixels (DIPs) wide and tall.

The `"default_icon"` key is a dictionary of sizes to image paths. Chrome uses these icons to choose which image scale to use. If an exact match is not found, Chrome selects the closest available and scales it to fit the image, which might affect image quality.

Because devices with less-common scale factors like 1.5x or 1.2x are becoming more common, we encourage you to provide multiple sizes for your icons. This also futureproofs your extension against potential icon display size changes. However, if only providing a single size, the `"default_icon"` key can also be set to a string with the path to a single icon instead of a dictionary.

You can also call `action.setIcon()` to set your extension's icon programmatically by specifying a different image path or providing a dynamically-generated icon using the HTML `canvas` element, or, if setting from an extension service worker, the `offscreen` canvas API.

```javascript
const canvas = new OffscreenCanvas(16, 16);
const context = canvas.getContext('2d');
context.clearRect(0, 0, 16, 16);
context.fillStyle = '#00FF00'; // Green
context.fillRect(0, 0, 16, 16);
const imageData = context.getImageData(0, 0, 16, 16);
chrome.action.setIcon({imageData: imageData}, () => { /* ... */ });
```

Note: The `action.setIcon()` API is intended to set a static image. Don't use animated images for your icons.

For packed extensions (installed from a `.crx` file), images can be in most formats that the Blink rendering engine can display, including `PNG`, `JPEG`, `BMP`, `ICO`, and others. `SVG` isn't supported. Unpacked extensions must use `PNG` images.

### Tooltip (title)

The tooltip, or title, appears when the user holds their mouse pointer over the extension's icon in the toolbar. It's also included in the accessible text spoken by screen readers when the button gets focus.

The default tooltip is set using the `"default_title"` field of the `"action"` key in `manifest.json`. You can also set it programmatically by calling `action.setTitle()`.

### Badge

Actions can optionally display a "badge" 鈥?a bit of text layered over the icon. This lets you update the action to display a small amount of information about the state of the extension, such as a counter. The badge has a text component and a background color. Because space is limited, we recommend that badge text use four or fewer characters.

To create a badge, set it programmatically by calling `action.setBadgeBackgroundColor()` and `action.setBadgeText()`. There isn't a default badge setting in the manifest. Badge color values can be either an array of four integers between 0 and 255 that make up the RGBA color of the badge or a string with a CSS color value.

```javascript
chrome.action.setBadgeBackgroundColor(
  {color: [0, 255, 0, 0]}, // Green
  () => { /* ... */ },
);
chrome.action.setBadgeBackgroundColor(
  {color: '#00FF00'}, // Also green
  () => { /* ... */ },
);
chrome.action.setBadgeBackgroundColor(
  {color: 'green'}, // Also, also green
  () => { /* ... */ },
);
```

### Popup

An action's popup is shown when the user clicks on the extension's action button in the toolbar. The popup can contain any HTML contents you like, and will be automatically sized to fit its contents. The popup's size must be between 25x25 and 800x600 pixels.

The popup is initially set by the `"default_popup"` property in the `"action"` key in the `manifest.json` file. If present, this property should point to a relative path within the extension directory. It can also be updated dynamically to point to a different relative path using the `action.setPopup()` method.

Note: The `action.onClicked` event won't be sent if the extension action has specified a popup to show on click of the current tab.

## Use cases

### Per-tab state

Extension actions can have different states for each tab. To set a value for an individual tab, use the `tabId` property in the `action` API's setting methods. For example, to set the badge text for a specific tab, do something like the following:

```javascript
function getTabId() { /* ... */}
function getTabBadge() { /* ... */}
chrome.action.setBadgeText(
  {
    text: getTabBadge(tabId),
    tabId: getTabId(),
  },
  () => { ... }
);
```

If the `tabId` property is left out, the setting is treated as a global setting. Tab-specific settings take priority over global settings.

### Enabled state

By default, toolbar actions are enabled (clickable) on every tab. You can change this default by setting the `default_state` property in the `action` key of the manifest. If `default_state` is set to `"disabled"`, the action is disabled by default and must be enabled programmatically to be clickable. If `default_state` is set to `"enabled"` (the default), the action is enabled and clickable by default.

You can control the state programmatically using the `action.enable()` and `action.disable()` methods. This only affects whether the popup (if any) or `action.onClicked` event is sent to your extension; it doesn't affect the action's presence in the toolbar.

## Examples

The following examples show some common ways that actions are used in extensions. To try this API, install the Action API example from the chrome-extension-samples repository.

### Show a popup

It's common for an extension to display a popup when the user clicks the extension's action. To implement this in your own extension, declare the popup in your `manifest.json` and specify the content that Chrome should display in the popup.

```json
// manifest.json
{
  "name": "Action popup demo",
  "version": "1.0",
  "manifest_version": 3,
  "action": {
    "default_title": "Click to view a popup",
    "default_popup": "popup.html"
  }
}
```

```html
<!-- popup.html -->
<!DOCTYPE html>
<html>
<head>
  <style>
    html {
      min-height: 5em;
      min-width: 10em;
      background: salmon;
    }
  </style>
</head>
<body>
  <p>Hello, world!</p>
</body>
</html>
```

### Inject a content script on click

A common pattern for extensions is to expose their primary feature using the extension's action. The following example demonstrates this pattern. When the user clicks the action, the extension injects a content script into the current page. The content script then displays an alert to verify that everything worked as expected.

```json
// manifest.json
{
  "name": "Action script injection demo",
  "version": "1.0",
  "manifest_version": 3,
  "action": {
    "default_title": "Click to show an alert"
  },
  "permissions": ["activeTab", "scripting"],
  "background": {
    "service_worker": "background.js"
  }
}
```

```javascript
// background.js
chrome.action.onClicked.addListener((tab) => {
  chrome.scripting.executeScript({
    target: {tabId: tab.id},
    files: ['content.js']
  });
});
```

```javascript
// content.js
alert('Hello, world!');
```

### Emulate actions with declarativeContent

This example shows how an extension's background logic can (a) disable an action by default and (b) use `declarativeContent` to enable the action on specific sites.

```javascript
// service-worker.js
// Wrap in an onInstalled callback to avoid unnecessary work
// every time the service worker is run
chrome.runtime.onInstalled.addListener(() => {
  // Page actions are disabled by default and enabled on select tabs
  chrome.action.disable();

  // Clear all rules to ensure only our expected rules are set
  chrome.declarativeContent.onPageChanged.removeRules(undefined, () => {
    // Declare a rule to enable the action on example.com pages
    let exampleRule = {
      conditions: [
        new chrome.declarativeContent.PageStateMatcher({
          pageUrl: {hostSuffix: '.example.com'},
        })
      ],
      actions: [new chrome.declarativeContent.ShowAction()],
    };

    // Finally, apply our new array of rules
    let rules = [exampleRule];
    chrome.declarativeContent.onPageChanged.addRules(rules);
  });
});
```

## Types

### `OpenPopupOptions`

Chrome 99+

#### Properties

*   `windowId`
    `number` optional
    The ID of the window to open the action popup in. Defaults to the currently-active window if unspecified.

### `TabDetails`

#### Properties

*   `tabId`
    `number` optional
    The ID of the tab to query state for. If no tab is specified, the non-tab-specific state is returned.

### `UserSettings`

Chrome 91+
The collection of user-specified settings relating to an extension's action.

#### Properties

*   `isOnToolbar`
    `boolean`
    Whether the extension's action icon is visible on browser windows' top-level toolbar (i.e., whether the extension has been 'pinned' by the user).

### `UserSettingsChange`

Chrome 130+

#### Properties

*   `isOnToolbar`
    `boolean` optional
    Whether the extension's action icon is visible on browser windows' top-level toolbar (i.e., whether the extension has been 'pinned' by the user).

## Methods

### `disable()`

Promise

```javascript
chrome.action.disable(
  tabId?: number,
  callback?: function,
)
```

Disables the action for a tab.

#### Parameters

*   `tabId`
    `number` optional
    The ID of the tab for which you want to modify the action.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `enable()`

Promise

```javascript
chrome.action.enable(
  tabId?: number,
  callback?: function,
)
```

Enables the action for a tab. By default, actions are enabled.

#### Parameters

*   `tabId`
    `number` optional
    The ID of the tab for which you want to modify the action.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getBadgeBackgroundColor()`

Promise

```javascript
chrome.action.getBadgeBackgroundColor(
  details: TabDetails,
  callback?: function,
)
```

Gets the background color of the action.

#### Parameters

*   `details`
    `TabDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (result: ColorArray) => void
    ```
    *   `result`
        `ColorArray`

#### Returns

*   `Promise<browserAction.ColorArray>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getBadgeText()`

Promise

```javascript
chrome.action.getBadgeText(
  details: TabDetails,
  callback?: function,
)
```

Gets the badge text of the action. If no tab is specified, the non-tab-specific badge text is returned. If `displayActionCountAsBadgeText` is enabled, a placeholder text will be returned unless the `declarativeNetRequestFeedback` permission is present or tab-specific badge text was provided.

#### Parameters

*   `details`
    `TabDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (result: string) => void
    ```
    *   `result`
        `string`

#### Returns

*   `Promise<string>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getBadgeTextColor()`

Promise Chrome 110+

```javascript
chrome.action.getBadgeTextColor(
  details: TabDetails,
  callback?: function,
)
```

Gets the text color of the action.

#### Parameters

*   `details`
    `TabDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (result: ColorArray) => void
    ```
    *   `result`
        `ColorArray`

#### Returns

*   `Promise<browserAction.ColorArray>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getPopup()`

Promise

```javascript
chrome.action.getPopup(
  details: TabDetails,
  callback?: function,
)
```

Gets the html document set as the popup for this action.

#### Parameters

*   `details`
    `TabDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (result: string) => void
    ```
    *   `result`
        `string`

#### Returns

*   `Promise<string>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getTitle()`

Promise

```javascript
chrome.action.getTitle(
  details: TabDetails,
  callback?: function,
)
```

Gets the title of the action.

#### Parameters

*   `details`
    `TabDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (result: string) => void
    ```
    *   `result`
        `string`

#### Returns

*   `Promise<string>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getUserSettings()`

Promise Chrome 91+

```javascript
chrome.action.getUserSettings(
  callback?: function,
)
```

Returns the user-specified settings relating to an extension's action.

#### Parameters

*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (userSettings: UserSettings) => void
    ```
    *   `userSettings`
        `UserSettings`

#### Returns

*   `Promise<UserSettings>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `isEnabled()`

Promise Chrome 110+

```javascript
chrome.action.isEnabled(
  tabId?: number,
  callback?: function,
)
```

Indicates whether the extension action is enabled for a tab (or globally if no `tabId` is provided). Actions enabled using only `declarativeContent` always return false.

#### Parameters

*   `tabId`
    `number` optional
    The ID of the tab for which you want check enabled status.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (isEnabled: boolean) => void
    ```
    *   `isEnabled`
        `boolean`
        True if the extension action is enabled.

#### Returns

*   `Promise<boolean>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `openPopup()`

Promise Chrome 127+

```javascript
chrome.action.openPopup(
  options?: OpenPopupOptions,
  callback?: function,
)
```

Opens the extension's popup. Between Chrome 118 and Chrome 126, this is only available to policy installed extensions.

#### Parameters

*   `options`
    `OpenPopupOptions` optional
    Specifies options for opening the popup.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setBadgeBackgroundColor()`

Promise

```javascript
chrome.action.setBadgeBackgroundColor(
  details: object,
  callback?: function,
)
```

Sets the background color for the badge.

#### Parameters

*   `details`
    `object`
    *   `color`
        `string | ColorArray`
        An array of four integers in the range [0,255] that make up the RGBA color of the badge. For example, opaque red is `[255, 0, 0, 255]`. Can also be a string with a CSS value, with opaque red being `#FF0000` or `#F00`.
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setBadgeText()`

Promise

```javascript
chrome.action.setBadgeText(
  details: object,
  callback?: function,
)
```

Sets the badge text for the action. The badge is displayed on top of the icon.

#### Parameters

*   `details`
    `object`
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
    *   `text`
        `string` optional
        Any number of characters can be passed, but only about four can fit in the space. If an empty string (`''`) is passed, the badge text is cleared. If `tabId` is specified and `text` is null, the text for the specified tab is cleared and defaults to the global badge text.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setBadgeTextColor()`

Promise Chrome 110+

```javascript
chrome.action.setBadgeTextColor(
  details: object,
  callback?: function,
)
```

Sets the text color for the badge.

#### Parameters

*   `details`
    `object`
    *   `color`
        `string | ColorArray`
        An array of four integers in the range [0,255] that make up the RGBA color of the badge. For example, opaque red is `[255, 0, 0, 255]`. Can also be a string with a CSS value, with opaque red being `#FF0000` or `#F00`. Not setting this value will cause a color to be automatically chosen that will contrast with the badge's background color so the text will be visible. Colors with alpha values equivalent to 0 will not be set and will return an error.
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setIcon()`

Promise

```javascript
chrome.action.setIcon(
  details: object,
  callback?: function,
)
```

Sets the icon for the action. The icon can be specified either as the path to an image file or as the pixel data from a canvas element, or as dictionary of either one of those. Either the `path` or the `imageData` property must be specified.

#### Parameters

*   `details`
    `object`
    *   `imageData`
        `ImageData | object` optional
        Either an `ImageData` object or a dictionary `{size -> ImageData}` representing icon to be set. If the icon is specified as a dictionary, the actual image to be used is chosen depending on screen's pixel density. If the number of image pixels that fit into one screen space unit equals `scale`, then image with size `scale * n` will be selected, where `n` is the size of the icon in the UI. At least one image must be specified. Note that `'details.imageData = foo'` is equivalent to `'details.imageData = {'16': foo}'`
    *   `path`
        `string | object` optional
        Either a relative image path or a dictionary `{size -> relative image path}` pointing to icon to be set. If the icon is specified as a dictionary, the actual image to be used is chosen depending on screen's pixel density. If the number of image pixels that fit into one screen space unit equals `scale`, then image with size `scale * n` will be selected, where `n` is the size of the icon in the UI. At least one image must be specified. Note that `'details.path = foo'` is equivalent to `'details.path = {'16': foo}'`
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setPopup()`

Promise

```javascript
chrome.action.setPopup(
  details: object,
  callback?: function,
)
```

Sets the HTML document to be opened as a popup when the user clicks on the action's icon.

#### Parameters

*   `details`
    `object`
    *   `popup`
        `string`
        The relative path to the HTML file to show in a popup. If set to the empty string (`''`), no popup is shown.
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setTitle()`

Promise

```javascript
chrome.action.setTitle(
  details: object,
  callback?: function,
)
```

Sets the title of the action. This shows up in the tooltip.

#### Parameters

*   `details`
    `object`
    *   `tabId`
        `number` optional
        Limits the change to when a particular tab is selected. Automatically resets when the tab is closed.
    *   `title`
        `string`
        The string the action should display when moused over.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onClicked`

```javascript
chrome.action.onClicked.addListener(
  callback: function,
)
```

Fired when an action icon is clicked. This event will not fire if the action has a popup.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (tab: tabs.Tab) => void
    ```
    *   `tab`
        `tabs.Tab`

### `onUserSettingsChanged`

Chrome 130+

```javascript
chrome.action.onUserSettingsChanged.addListener(
  callback: function,
)
```

Fired when user-specified settings relating to an extension's action change.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (change: UserSettingsChange) => void
    ```
    *   `change`
        `UserSettingsChange`

===

---
title: chrome.alarms
url: https://developer.chrome.com/docs/extensions/reference/api/alarms
---

# chrome.alarms

Chrome 120: Starting in Chrome 120, the minimum alarm interval has been reduced from 1 minute to 30 seconds. For an alarm to trigger in 30 seconds, set `periodInMinutes: 0.5`. Chrome 117: Starting in Chrome 117, the number of active alarms is limited to 500. Once this limit is reached, `chrome.alarms.create()` will fail. When using a callback, `chrome.runtime.lastError` will be set. When using promises, the promise will be rejected.

## Description

Use the `chrome.alarms` API to schedule code to run periodically or at a specified time in the future.

## Permissions

`alarms`

To use the `chrome.alarms` API, declare the `"alarms"` permission in the manifest:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "alarms"
  ],
  ...
}
```

## Concepts and usage

To ensure reliable behavior, it is helpful to understand how the API behaves.

### Device sleep

Alarms continue to run while a device is sleeping. However, an alarm will not wake up a device. When the device wakes up, any missed alarms will fire. Repeating alarms will fire at most once and then be rescheduled using the specified period starting from when the device wakes, not taking into account any time that has already elapsed since the alarm was originally set to run.

### Persistence

Alarms generally persist until an extension is updated. However, this is not guaranteed, and alarms may be cleared when the browser is restarted. Consequently, consider setting a value in storage when an alarm is created, and then ensure it exists each time your service worker starts up. For example:

```javascript
const STORAGE_KEY = "user-preference-alarm-enabled";

async function checkAlarmState() {
  const { alarmEnabled } = await chrome.storage.get(STORAGE_KEY);
  if (alarmEnabled) {
    const alarm = await chrome.alarms.get("my-alarm");
    if (!alarm) {
      await chrome.alarms.create({ periodInMinutes: 1 });
    }
  }
}

checkAlarmState();
```

## Examples

The following examples show how to use and respond to an alarm. To try this API, install the Alarm API example from the chrome-extension-samples repository.

### Set an alarm

The following example sets an alarm in the service worker when the extension is installed:

service-worker.js:

```javascript
chrome.runtime.onInstalled.addListener(async ({ reason }) => {
  if (reason !== 'install') {
    return;
  }
  // Create an alarm so we have something to look at in the demo
  await chrome.alarms.create('demo-default-alarm', {
    delayInMinutes: 1,
    periodInMinutes: 1
  });
});
```

### Respond to an alarm

The following example sets the action toolbar icon based on the name of the alarm that went off.

service-worker.js:

```javascript
chrome.alarms.onAlarm.addListener((alarm) => {
  chrome.action.setIcon({
    path: getIconPath(alarm.name),
  });
});
```

## Types

### `Alarm`

#### Properties

*   `name`
    `string`
    Name of this alarm.
*   `periodInMinutes`
    `number` optional
    If not null, the alarm is a repeating alarm and will fire again in `periodInMinutes` minutes.
*   `scheduledTime`
    `number`
    Time at which this alarm was scheduled to fire, in milliseconds past the epoch (e.g. `Date.now() + n`). For performance reasons, the alarm may have been delayed an arbitrary amount beyond this.

### `AlarmCreateInfo`

#### Properties

*   `delayInMinutes`
    `number` optional
    Length of time in minutes after which the `onAlarm` event should fire.
*   `periodInMinutes`
    `number` optional
    If set, the `onAlarm` event should fire every `periodInMinutes` minutes after the initial event specified by `when` or `delayInMinutes`. If not set, the alarm will only fire once.
*   `when`
    `number` optional
    Time at which the alarm should fire, in milliseconds past the epoch (e.g. `Date.now() + n`).

## Methods

### `clear()`

Promise

```javascript
chrome.alarms.clear(
  name?: string,
  callback?: function,
)
```

Clears the alarm with the given name.

#### Parameters

*   `name`
    `string` optional
    The name of the alarm to clear. Defaults to the empty string.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (wasCleared: boolean) => void
    ```
    *   `wasCleared`
        `boolean`

#### Returns

*   `Promise<boolean>`
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `clearAll()`

Promise

```javascript
chrome.alarms.clearAll(
  callback?: function,
)
```

Clears all alarms.

#### Parameters

*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (wasCleared: boolean) => void
    ```
    *   `wasCleared`
        `boolean`

#### Returns

*   `Promise<boolean>`
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `create()`

Promise

```javascript
chrome.alarms.create(
  name?: string,
  alarmInfo: AlarmCreateInfo,
  callback?: function,
)
```

Creates an alarm. Near the time(s) specified by `alarmInfo`, the `onAlarm` event is fired. If there is another alarm with the same name (or no name if none is specified), it will be cancelled and replaced by this alarm.

In order to reduce the load on the user's machine, Chrome limits alarms to at most once every 30 seconds but may delay them an arbitrary amount more. That is, setting `delayInMinutes` or `periodInMinutes` to less than 0.5 will not be honored and will cause a warning. `when` can be set to less than 30 seconds after "now" without warning but won't actually cause the alarm to fire for at least 30 seconds.

To help you debug your app or extension, when you've loaded it unpacked, there's no limit to how often the alarm can fire.

#### Parameters

*   `name`
    `string` optional
    Optional name to identify this alarm. Defaults to the empty string.
*   `alarmInfo`
    `AlarmCreateInfo`
    Describes when the alarm should fire. The initial time must be specified by either `when` or `delayInMinutes` (but not both). If `periodInMinutes` is set, the alarm will repeat every `periodInMinutes` minutes after the initial event. If neither `when` or `delayInMinutes` is set for a repeating alarm, `periodInMinutes` is used as the default for `delayInMinutes`.
*   `callback`
    `function` optional
    Chrome 111+
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `get()`

Promise

```javascript
chrome.alarms.get(
  name?: string,
  callback?: function,
)
```

Retrieves details about the specified alarm.

#### Parameters

*   `name`
    `string` optional
    The name of the alarm to get. Defaults to the empty string.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (alarm?: Alarm) => void
    ```
    *   `alarm`
        `Alarm` optional

#### Returns

*   `Promise<Alarm | undefined>`
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAll()`

Promise

```javascript
chrome.alarms.getAll(
  callback?: function,
)
```

Gets an array of all the alarms.

#### Parameters

*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (alarms: Alarm[]) => void
    ```
    *   `alarms`
        `Alarm[]`

#### Returns

*   `Promise<Alarm[]>`
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onAlarm`

```javascript
chrome.alarms.onAlarm.addListener(
  callback: function,
)
```

Fired when an alarm has elapsed. Useful for event pages.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (alarm: Alarm) => void
    ```
    *   `alarm`
        `Alarm`

===

---
title: API reference
url: https://developer.chrome.com/docs/extensions/reference/api/
---

Most extensions need access to one or more Chrome Extensions APIs to function. This API reference describes the APIs available for use in extensions and presents example use cases.

## Common Extensions API features

An Extensions API consists of a namespace containing methods and properties for doing extensions work, and usually, but not always, manifest fields for the `manifest.json` file. For example, the `chrome.action` namespace requires an `"action"` object in the manifest. Many APIs also require permissions in the manifest.

Methods in extension APIs are **asynchronous** unless stated otherwise. Asynchronous methods return immediately, without waiting for the operation that calls them to finish. Use promises to get the results of these asynchronous methods.

Manifest V3 is supported generally in Chrome 88 or later. For extension features added in later Chrome versions, see the API reference documentation for support information. If your extension requires a specific API, you can specify a minimum chrome version in the manifest file.

## Chrome Extension APIs

[`accessibilityFeatures`](https://developer.chrome.com/docs/extensions/reference/api/accessibilityFeatures)
:   Use the `chrome.accessibilityFeatures` API to manage Chrome's accessibility features. This API relies on the `ChromeSetting` prototype of the type API for getting and setting individual accessibility features. In order to get feature states the extension must request `accessibilityFeatures.read` permission. For modifying feature state, the extension needs `accessibilityFeatures.modify` permission. Note that `accessibilityFeatures.modify` does not imply `accessibilityFeatures.read` permission.

[`action`](https://developer.chrome.com/docs/extensions/reference/api/action)
:   Chrome 88+ MV3+

    Use the `chrome.action` API to control the extension's icon in the Google Chrome toolbar.

[`alarms`](https://developer.chrome.com/docs/extensions/reference/api/alarms)
:   Use the `chrome.alarms` API to schedule code to run periodically or at a specified time in the future.

[`audio`](https://developer.chrome.com/docs/extensions/reference/api/audio)
:   Chrome 59+ ChromeOS only

    The `chrome.audio` API is provided to allow users to get information about and control the audio devices attached to the system. This API is currently only available in kiosk mode for ChromeOS.

[`bookmarks`](https://developer.chrome.com/docs/extensions/reference/api/bookmarks)
:   Use the `chrome.bookmarks` API to create, organize, and otherwise manipulate bookmarks. Also see Override Pages, which you can use to create a custom Bookmark Manager page.

[`browsingData`](https://developer.chrome.com/docs/extensions/reference/api/browsingData)
:   Use the `chrome.browsingData` API to remove browsing data from a user's local profile.

[`certificateProvider`](https://developer.chrome.com/docs/extensions/reference/api/certificateProvider)
:   Chrome 46+ ChromeOS only

    Use this API to expose certificates to the platform which can use these certificates for TLS authentications.

[`commands`](https://developer.chrome.com/docs/extensions/reference/api/commands)
:   Use the `commands` API to add keyboard shortcuts that trigger actions in your extension, for example, an action to open the browser action or send a command to the extension.

[`contentSettings`](https://developer.chrome.com/docs/extensions/reference/api/contentSettings)
:   Use the `chrome.contentSettings` API to change settings that control whether websites can use features such as cookies, JavaScript, and plugins. More generally speaking, content settings allow you to customize Chrome's behavior on a per-site basis instead of globally.

[`contextMenus`](https://developer.chrome.com/docs/extensions/reference/api/contextMenus)
:   Use the `chrome.contextMenus` API to add items to Google Chrome's context menu. You can choose what types of objects your context menu additions apply to, such as images, hyperlinks, and pages.

[`cookies`](https://developer.chrome.com/docs/extensions/reference/api/cookies)
:   Use the `chrome.cookies` API to query and modify cookies, and to be notified when they change.

[`debugger`](https://developer.chrome.com/docs/extensions/reference/api/debugger)
:   The `chrome.debugger` API serves as an alternate transport for Chrome's remote debugging protocol. Use `chrome.debugger` to attach to one or more tabs to instrument network interaction, debug JavaScript, mutate the DOM and CSS, and more. Use the Debuggee property `tabId` to target tabs with `sendCommand` and route events by `tabId` from `onEvent` callbacks.

[`declarativeContent`](https://developer.chrome.com/docs/extensions/reference/api/declarativeContent)
:   Use the `chrome.declarativeContent` API to take actions depending on the content of a page, without requiring permission to read the page's content.

[`declarativeNetRequest`](https://developer.chrome.com/docs/extensions/reference/api/declarativeNetRequest)
:   Chrome 84+

    The `chrome.declarativeNetRequest` API is used to block or modify network requests by specifying declarative rules. This lets extensions modify network requests without intercepting them and viewing their content, thus providing more privacy.

[`desktopCapture`](https://developer.chrome.com/docs/extensions/reference/api/desktopCapture)
:   The Desktop Capture API captures the content of the screen, individual windows, or individual tabs.

[`devtools.inspectedWindow`](https://developer.chrome.com/docs/extensions/reference/api/devtools/inspectedWindow)
:   Use the `chrome.devtools.inspectedWindow` API to interact with the inspected window: obtain the tab ID for the inspected page, evaluate the code in the context of the inspected window, reload the page, or obtain the list of resources within the page.

[`devtools.network`](https://developer.chrome.com/docs/extensions/reference/api/devtools/network)
:   Use the `chrome.devtools.network` API to retrieve the information about network requests displayed by the Developer Tools in the Network panel.

[`devtools.panels`](https://developer.chrome.com/docs/extensions/reference/api/devtools/panels)
:   Use the `chrome.devtools.panels` API to integrate your extension into Developer Tools window UI: create your own panels, access existing panels, and add sidebars.

[`devtools.performance`](https://developer.chrome.com/docs/extensions/reference/api/devtools/performance)
:   Chrome 129+

    Use the `chrome.devtools.performance` API to listen to recording status updates in the Performance panel in DevTools.

[`devtools.recorder`](https://developer.chrome.com/docs/extensions/reference/api/devtools/recorder)
:   Chrome 105+

    Use the `chrome.devtools.recorder` API to customize the Recorder panel in DevTools.

[`dns`](https://developer.chrome.com/docs/extensions/reference/api/dns)
:   Dev channel

    Use the `chrome.dns` API for dns resolution.

[`documentScan`](https://developer.chrome.com/docs/extensions/reference/api/documentScan)
:   Chrome 44+ ChromeOS only

    Use the `chrome.documentScan` API to discover and retrieve images from attached document scanners.

[`dom`](https://developer.chrome.com/docs/extensions/reference/api/dom)
:   Chrome 88+

    Use the `chrome.dom` API to access special DOM APIs for Extensions

[`downloads`](https://developer.chrome.com/docs/extensions/reference/api/downloads)
:   Use the `chrome.downloads` API to programmatically initiate, monitor, manipulate, and search for downloads.

[`enterprise.deviceAttributes`](https://developer.chrome.com/docs/extensions/reference/api/enterprise/deviceAttributes)
:   Chrome 46+ ChromeOS only Requires policy

    Use the `chrome.enterprise.deviceAttributes` API to read device attributes. Note: This API is only available to extensions force-installed by enterprise policy.

[`enterprise.hardwarePlatform`](https://developer.chrome.com/docs/extensions/reference/api/enterprise/hardwarePlatform)
:   Chrome 71+ Requires policy

    Use the `chrome.enterprise.hardwarePlatform` API to get the manufacturer and model of the hardware platform where the browser runs. Note: This API is only available to extensions installed by enterprise policy.

[`enterprise.networkingAttributes`](https://developer.chrome.com/docs/extensions/reference/api/enterprise/networkingAttributes)
:   Chrome 85+ ChromeOS only Requires policy

    Use the `chrome.enterprise.networkingAttributes` API to read information about your current network. Note: This API is only available to extensions force-installed by enterprise policy.

[`enterprise.platformKeys`](https://developer.chrome.com/docs/extensions/reference/api/enterprise/platformKeys)
:   ChromeOS only Requires policy

    Use the `chrome.enterprise.platformKeys` API to generate keys and install certificates for these keys. The certificates will be managed by the platform and can be used for TLS authentication, network access or by other extension through `chrome.platformKeys`.

[`events`](https://developer.chrome.com/docs/extensions/reference/api/events)
:   The `chrome.events` namespace contains common types used by APIs dispatching events to notify you when something interesting happens.

[`extension`](https://developer.chrome.com/docs/extensions/reference/api/extension)
:   The `chrome.extension` API has utilities that can be used by any extension page. It includes support for exchanging messages between an extension and its content scripts or between extensions, as described in detail in Message Passing.

[`extensionTypes`](https://developer.chrome.com/docs/extensions/reference/api/extensionTypes)
:   The `chrome.extensionTypes` API contains type declarations for Chrome extensions.

[`fileBrowserHandler`](https://developer.chrome.com/docs/extensions/reference/api/fileBrowserHandler)
:   ChromeOS only Foreground only

    Use the `chrome.fileBrowserHandler` API to extend the Chrome OS file browser. For example, you can use this API to enable users to upload files to your website.

[`fileSystemProvider`](https://developer.chrome.com/docs/extensions/reference/api/fileSystemProvider)
:   ChromeOS only

    Use the `chrome.fileSystemProvider` API to create file systems, that can be accessible from the file manager on Chrome OS.

[`fontSettings`](https://developer.chrome.com/docs/extensions/reference/api/fontSettings)
:   Use the `chrome.fontSettings` API to manage Chrome's font settings.

[`gcm`](https://developer.chrome.com/docs/extensions/reference/api/gcm)
:   Use `chrome.gcm` to enable apps and extensions to send and receive messages through Firebase Cloud Messaging (FCM).

[`history`](https://developer.chrome.com/docs/extensions/reference/api/history)
:   Use the `chrome.history` API to interact with the browser's record of visited pages. You can add, remove, and query for URLs in the browser's history. To override the history page with your own version, see Override Pages.

[`i18n`](https://developer.chrome.com/docs/extensions/reference/api/i18n)
:   Use the `chrome.i18n` infrastructure to implement internationalization across your whole app or extension.

[`identity`](https://developer.chrome.com/docs/extensions/reference/api/identity)
:   Use the `chrome.identity` API to get OAuth2 access tokens.

[`idle`](https://developer.chrome.com/docs/extensions/reference/api/idle)
:   Use the `chrome.idle` API to detect when the machine's idle state changes.

[`input.ime`](https://developer.chrome.com/docs/extensions/reference/api/input/ime)
:   ChromeOS only

    Use the `chrome.input.ime` API to implement a custom IME for Chrome OS. This allows your extension to handle keystrokes, set the composition, and manage the candidate window.

[`instanceID`](https://developer.chrome.com/docs/extensions/reference/api/instanceID)
:   Chrome 44+

    Use `chrome.instanceID` to access the Instance ID service.

[`loginState`](https://developer.chrome.com/docs/extensions/reference/api/loginState)
:   Chrome 78+ ChromeOS only

    Use the `chrome.loginState` API to read and monitor the login state.

[`management`](https://developer.chrome.com/docs/extensions/reference/api/management)
:   The `chrome.management` API provides ways to manage installed apps and extensions.

[`notifications`](https://developer.chrome.com/docs/extensions/reference/api/notifications)
:   Use the `chrome.notifications` API to create rich notifications using templates and show these notifications to users in the system tray.

[`offscreen`](https://developer.chrome.com/docs/extensions/reference/api/offscreen)
:   Chrome 109+ MV3+

    Use the `offscreen` API to create and manage offscreen documents.

[`omnibox`](https://developer.chrome.com/docs/extensions/reference/api/omnibox)
:   The `omnibox` API allows you to register a keyword with Google Chrome's address bar, which is also known as the omnibox.

[`pageCapture`](https://developer.chrome.com/docs/extensions/reference/api/pageCapture)
:   Use the `chrome.pageCapture` API to save a tab as MHTML.

[`permissions`](https://developer.chrome.com/docs/extensions/reference/api/permissions)
:   Use the `chrome.permissions` API to request declared optional permissions at run time rather than install time, so users understand why the permissions are needed and grant only those that are necessary.

[`platformKeys`](https://developer.chrome.com/docs/extensions/reference/api/platformKeys)
:   Chrome 45+ ChromeOS only

    Use the `chrome.platformKeys` API to access client certificates managed by the platform. If the user or policy grants the permission, an extension can use such a certficate in its custom authentication protocol. E.g. this allows usage of platform managed certificates in third party VPNs (see `chrome.vpnProvider`).

[`power`](https://developer.chrome.com/docs/extensions/reference/api/power)
:   Use the `chrome.power` API to override the system's power management features.

[`printerProvider`](https://developer.chrome.com/docs/extensions/reference/api/printerProvider)
:   Chrome 44+

    The `chrome.printerProvider` API exposes events used by print manager to query printers controlled by extensions, to query their capabilities and to submit print jobs to these printers.

[`printing`](https://developer.chrome.com/docs/extensions/reference/api/printing)
:   Chrome 81+ ChromeOS only

    Use the `chrome.printing` API to send print jobs to printers installed on Chromebook.

[`printingMetrics`](https://developer.chrome.com/docs/extensions/reference/api/printingMetrics)
:   Chrome 79+ ChromeOS only Requires policy

    Use the `chrome.printingMetrics` API to fetch data about printing usage.

[`privacy`](https://developer.chrome.com/docs/extensions/reference/api/privacy)
:   Use the `chrome.privacy` API to control usage of the features in Chrome that can affect a user's privacy. This API relies on the `ChromeSetting` prototype of the type API for getting and setting Chrome's configuration.

[`processes`](https://developer.chrome.com/docs/extensions/reference/api/processes)
:   Dev channel

    Use the `chrome.processes` API to interact with the browser's processes.

[`proxy`](https://developer.chrome.com/docs/extensions/reference/api/proxy)
:   Use the `chrome.proxy` API to manage Chrome's proxy settings. This API relies on the `ChromeSetting` prototype of the type API for getting and setting the proxy configuration.

[`readingList`](https://developer.chrome.com/docs/extensions/reference/api/readingList)
:   Chrome 120+ MV3+

    Use the `chrome.readingList` API to read from and modify the items in the Reading List.

[`runtime`](https://developer.chrome.com/docs/extensions/reference/api/runtime)
:   Use the `chrome.runtime` API to retrieve the service worker, return details about the manifest, and listen for and respond to events in the extension lifecycle. You can also use this API to convert the relative path of URLs to fully-qualified URLs.

[`scripting`](https://developer.chrome.com/docs/extensions/reference/api/scripting)
:   Chrome 88+ MV3+

    Use the `chrome.scripting` API to execute script in different contexts.

[`search`](https://developer.chrome.com/docs/extensions/reference/api/search)
:   Chrome 87+

    Use the `chrome.search` API to search via the default provider.

[`sessions`](https://developer.chrome.com/docs/extensions/reference/api/sessions)
:   Use the `chrome.sessions` API to query and restore tabs and windows from a browsing session.

[`sidePanel`](https://developer.chrome.com/docs/extensions/reference/api/sidePanel)
:   Chrome 114+ MV3+

    Use the `chrome.sidePanel` API to host content in the browser's side panel alongside the main content of a webpage.

[`storage`](https://developer.chrome.com/docs/extensions/reference/api/storage)
:   Use the `chrome.storage` API to store, retrieve, and track changes to user data.

[`system.cpu`](https://developer.chrome.com/docs/extensions/reference/api/system/cpu)
:   Use the `system.cpu` API to query CPU metadata.

[`system.display`](https://developer.chrome.com/docs/extensions/reference/api/system/display)
:   Use the `system.display` API to query display metadata.

[`system.memory`](https://developer.chrome.com/docs/extensions/reference/api/system/memory)
:   The `chrome.system.memory` API.

[`system.storage`](https://developer.chrome.com/docs/extensions/reference/api/system/storage)
:   Use the `chrome.system.storage` API to query storage device information and be notified when a removable storage device is attached and detached.

[`systemLog`](https://developer.chrome.com/docs/extensions/reference/api/systemLog)
:   Chrome 125+ ChromeOS only Requires policy

    Use the `chrome.systemLog` API to record Chrome system logs from extensions.

[`tabCapture`](https://developer.chrome.com/docs/extensions/reference/api/tabCapture)
:   Use the `chrome.tabCapture` API to interact with tab media streams.

[`tabGroups`](https://developer.chrome.com/docs/extensions/reference/api/tabGroups)
:   Chrome 89+ MV3+

    Use the `chrome.tabGroups` API to interact with the browser's tab grouping system. You can use this API to modify and rearrange tab groups in the browser. To group and ungroup tabs, or to query what tabs are in groups, use the `chrome.tabs` API.

[`tabs`](https://developer.chrome.com/docs/extensions/reference/api/tabs)
:   Use the `chrome.tabs` API to interact with the browser's tab system. You can use this API to create, modify, and rearrange tabs in the browser.

[`topSites`](https://developer.chrome.com/docs/extensions/reference/api/topSites)
:   Use the `chrome.topSites` API to access the top sites (i.e. most visited sites) that are displayed on the new tab page. These do not include shortcuts customized by the user.

[`tts`](https://developer.chrome.com/docs/extensions/reference/api/tts)
:   Use the `chrome.tts` API to play synthesized text-to-speech (TTS). See also the related `ttsEngine` API, which allows an extension to implement a speech engine.

[`ttsEngine`](https://developer.chrome.com/docs/extensions/reference/api/ttsEngine)
:   Use the `chrome.ttsEngine` API to implement a text-to-speech(TTS) engine using an extension. If your extension registers using this API, it will receive events containing an utterance to be spoken and other parameters when any extension or Chrome App uses the `tts` API to generate speech. Your extension can then use any available web technology to synthesize and output the speech, and send events back to the calling function to report the status.

[`types`](https://developer.chrome.com/docs/extensions/reference/api/types)
:   The `chrome.types` API contains type declarations for Chrome.

[`userScripts`](https://developer.chrome.com/docs/extensions/reference/api/userScripts)
:   Chrome 120+ MV3+

    Use the `userScripts` API to execute user scripts in the User Scripts context.

[`vpnProvider`](https://developer.chrome.com/docs/extensions/reference/api/vpnProvider)
:   Chrome 43+ ChromeOS only

    Use the `chrome.vpnProvider` API to implement a VPN client.

[`wallpaper`](https://developer.chrome.com/docs/extensions/reference/api/wallpaper)
:   Chrome 43+ ChromeOS only

    Use the `chrome.wallpaper` API to change the ChromeOS wallpaper.

[`webAuthenticationProxy`](https://developer.chrome.com/docs/extensions/reference/api/webAuthenticationProxy)
:   Chrome 115+ MV3+

    The `chrome.webAuthenticationProxy` API lets remote desktop software running on a remote host intercept Web Authentication API (WebAuthn) requests in order to handle them on a local client.

[`webNavigation`](https://developer.chrome.com/docs/extensions/reference/api/webNavigation)
:   Use the `chrome.webNavigation` API to receive notifications about the status of navigation requests in-flight.

[`webRequest`](https://developer.chrome.com/docs/extensions/reference/api/webRequest)
:   Use the `chrome.webRequest` API to observe and analyze traffic and to intercept, block, or modify requests in-flight.

[`windows`](https://developer.chrome.com/docs/extensions/reference/api/windows)
:   Use the `chrome.windows` API to interact with browser windows. You can use this API to create, modify, and rearrange windows in the browser. 

===

---
title: chrome.audio
url: https://developer.chrome.com/docs/extensions/reference/api/audio
---

# chrome.audio

Important: This API works only on ChromeOS.

## Description

The `chrome.audio` API is provided to allow users to get information about and control the audio devices attached to the system. This API is currently only available in kiosk mode for ChromeOS.

## Permissions

`audio`

## Availability

Chrome 59+ ChromeOS only

## Types

### `AudioDeviceInfo`

#### Properties

*   `deviceName`
    `string`
    Device name.
*   `deviceType`
    `DeviceType`
    Type of the device.
*   `displayName`
    `string`
    The user-friendly name (e.g. "USB Microphone").
*   `id`
    `string`
    The unique identifier of the audio device.
*   `isActive`
    `boolean`
    True if this is the current active device.
*   `level`
    `number`
    The sound level of the device, volume for output, gain for input.
*   `stableDeviceId`
    `string` optional
    The stable/persisted device id string when available.
*   `streamType`
    `StreamType`
    Stream type associated with this device.

### `DeviceFilter`

#### Properties

*   `isActive`
    `boolean` optional
    If set, only audio devices whose active state matches this value will satisfy the filter.
*   `streamTypes`
    `StreamType[]` optional
    If set, only audio devices whose stream type is included in this list will satisfy the filter.

### `DeviceIdLists`

#### Properties

*   `input`
    `string[]` optional
    List of input devices specified by their ID.
    To indicate input devices should be unaffected, leave this property unset.
*   `output`
    `string[]` optional
    List of output devices specified by their ID.
    To indicate output devices should be unaffected, leave this property unset.

### `DeviceProperties`

#### Properties

*   `level`
    `number` optional
    The audio device's desired sound level. Defaults to the device's current sound level.
    If used with audio input device, represents audio device gain.
    If used with audio output device, represents audio device volume.

### `DeviceType`

Available audio device types.

#### Enum

`"HEADPHONE"`
`"MIC"`
`"USB"`
`"BLUETOOTH"`
`"HDMI"`
`"INTERNAL_SPEAKER"`
`"INTERNAL_MIC"`
`"FRONT_MIC"`
`"REAR_MIC"`
`"KEYBOARD_MIC"`
`"HOTWORD"`
`"LINEOUT"`
`"POST_MIX_LOOPBACK"`
`"POST_DSP_LOOPBACK"`
`"ALSA_LOOPBACK"`
`"OTHER"`

### `LevelChangedEvent`

#### Properties

*   `deviceId`
    `string`
    ID of device whose sound level has changed.
*   `level`
    `number`
    The device's new sound level.

### `MuteChangedEvent`

#### Properties

*   `isMuted`
    `boolean`
    Whether or not the stream is now muted.
*   `streamType`
    `StreamType`
    The type of the stream for which the mute value changed. The updated mute value applies to all devices with this stream type.

### `StreamType`

Type of stream an audio device provides.

#### Enum

`"INPUT"`
`"OUTPUT"`

## Methods

### `getDevices()`

Promise

```javascript
chrome.audio.getDevices(
  filter?: DeviceFilter,
  callback?: function,
)
```

Gets a list of audio devices filtered based on `filter`.

#### Parameters

*   `filter`
    `DeviceFilter` optional
    Device properties by which to filter the list of returned audio devices. If the filter is not set or set to `{}`, returned device list will contain all available audio devices.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (devices: AudioDeviceInfo[]) => void
    ```
    *   `devices`
        `AudioDeviceInfo[]`

#### Returns

*   `Promise<AudioDeviceInfo[]>`
    Chrome 116+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getMute()`

Promise

```javascript
chrome.audio.getMute(
  streamType: StreamType,
  callback?: function,
)
```

Gets the system-wide mute state for the specified stream type.

#### Parameters

*   `streamType`
    `StreamType`
    Stream type for which mute state should be fetched.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (value: boolean) => void
    ```
    *   `value`
        `boolean`

#### Returns

*   `Promise<boolean>`
    Chrome 116+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setActiveDevices()`

Promise

```javascript
chrome.audio.setActiveDevices(
  ids: DeviceIdLists,
  callback?: function,
)
```

Sets lists of active input and/or output devices.

#### Parameters

*   `ids`
    `DeviceIdLists`
    Specifies IDs of devices that should be active. If either the input or output list is not set, devices in that category are unaffected.
    It is an error to pass in a non-existent device ID.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 116+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setMute()`

Promise

```javascript
chrome.audio.setMute(
  streamType: StreamType,
  isMuted: boolean,
  callback?: function,
)
```

Sets mute state for a stream type. The mute state will apply to all audio devices with the specified audio stream type.

#### Parameters

*   `streamType`
    `StreamType`
    Stream type for which mute state should be set.
*   `isMuted`
    `boolean`
    New mute value.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 116+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setProperties()`

Promise

```javascript
chrome.audio.setProperties(
  id: string,
  properties: DeviceProperties,
  callback?: function,
)
```

Sets the properties for the input or output device.

#### Parameters

*   `id`
    `string`
*   `properties`
    `DeviceProperties`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 116+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onDeviceListChanged`

```javascript
chrome.audio.onDeviceListChanged.addListener(
  callback: function,
)
```

Fired when audio devices change, either new devices being added, or existing devices being removed.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (devices: AudioDeviceInfo[]) => void
    ```
    *   `devices`
        `AudioDeviceInfo[]`

### `onLevelChanged`

```javascript
chrome.audio.onLevelChanged.addListener(
  callback: function,
)
```

Fired when sound level changes for an active audio device.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (event: LevelChangedEvent) => void
    ```
    *   `event`
        `LevelChangedEvent`

### `onMuteChanged`

```javascript
chrome.audio.onMuteChanged.addListener(
  callback: function,
)
```

Fired when the mute state of the audio input or output changes. Note that mute state is system-wide and the new value applies to every audio device with specified stream type.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (event: MuteChangedEvent) => void
    ```
    *   `event`
        `MuteChangedEvent`

===

---
title: chrome.bookmarks
url: https://developer.chrome.com/docs/extensions/reference/api/bookmarks
---

# chrome.bookmarks

## Description

Use the `chrome.bookmarks` API to create, organize, and otherwise manipulate bookmarks. Also see `Override Pages`, which you can use to create a custom Bookmark Manager page.

## Permissions

`bookmarks`

You must declare the `"bookmarks"` permission in the extension manifest to use the bookmarks API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "bookmarks"
  ],
  ...
}
```

## Concepts and usage

### Objects and properties

Bookmarks are organized in a tree, where each node in the tree is either a bookmark or a folder (sometimes called a group). Each node in the tree is represented by a `bookmarks.BookmarkTreeNode` object.

`BookmarkTreeNode` properties are used throughout the `chrome.bookmarks` API. For example, when you call `bookmarks.create`, you pass in the new node's parent (`parentId`), and, optionally, the node's `index`, `title`, and `url` properties. See `bookmarks.BookmarkTreeNode` for information about the properties a node can have.

Note: You cannot use this API to add or remove entries in the root folder. You also cannot rename, move, or remove the special "Bookmarks Bar" and "Other Bookmarks" folders.

### Examples

The following code creates a folder with the title "Extension bookmarks". The first argument to `create()` specifies properties for the new folder. The second argument defines a function to be executed after the folder is created.

```javascript
chrome.bookmarks.create({
  'parentId': bookmarkBar.id,
  'title': 'Extension bookmarks'
}, function(newFolder) {
  console.log("added folder: " + newFolder.title);
});
```

The next snippet creates a bookmark pointing to the developer documentation for extensions. Since nothing bad will happen if creating the bookmark fails, this code doesn't bother to define a callback function.

```javascript
chrome.bookmarks.create({
  'parentId': extensionsFolderId,
  'title': 'Extensions doc',
  'url': 'https://developer.chrome.com/docs/extensions'
});
```

To try this API, install the Bookmarks API example from the `chrome-extension-samples` repository.

## Types

### `BookmarkTreeNode`

A node (either a bookmark or a folder) in the bookmark tree. Child nodes are ordered within their parent folder.

#### Properties

*   `children`

    `BookmarkTreeNode[]` optional

    An ordered list of children of this node.
*   `dateAdded`

    `number` optional

    When this node was created, in milliseconds since the epoch (`new Date(dateAdded)`).
*   `dateGroupModified`

    `number` optional

    When the contents of this folder last changed, in milliseconds since the epoch.
*   `dateLastUsed`

    `number` optional

    Chrome 114+

    When this node was last opened, in milliseconds since the epoch. Not set for folders.
*   `folderType`

    `FolderType` optional

    Chrome 134+

    If present, this is a folder that is added by the browser and that cannot be modified by the user or the extension. Child nodes may be modified, if this node does not have the `unmodifiable` property set. Omitted if the node can be modified by the user and the extension (default).

    There may be zero, one or multiple nodes of each folder type. A folder may be added or removed by the browser, but not via the extensions API.
*   `id`

    `string`

    The unique identifier for the node. IDs are unique within the current profile, and they remain valid even after the browser is restarted.
*   `index`

    `number` optional

    The 0-based position of this node within its parent folder.
*   `parentId`

    `string` optional

    The `id` of the parent folder. Omitted for the root node.
*   `syncing`

    `boolean`

    Chrome 134+

    Whether this node is synced with the user's remote account storage by the browser. This can be used to distinguish between account and local-only versions of the same `FolderType`. The value of this property may change for an existing node, for example as a result of user action.

    Note: this reflects whether the node is saved to the browser's built-in account provider. It is possible that a node could be synced via a third-party, even if this value is `false`.

    For managed nodes (nodes where `unmodifiable` is set to `true`), this property will always be `false`.
*   `title`

    `string`

    The text displayed for the node.
*   `unmodifiable`

    `"managed"` optional

    Indicates the reason why this node is unmodifiable. The `managed` value indicates that this node was configured by the system administrator or by the custodian of a supervised user. Omitted if the node can be modified by the user and the extension (default).
*   `url`

    `string` optional

    The URL navigated to when a user clicks the bookmark. Omitted for folders.

### `BookmarkTreeNodeUnmodifiable`

Chrome 44+

Indicates the reason why this node is unmodifiable. The `managed` value indicates that this node was configured by the system administrator. Omitted if the node can be modified by the user and the extension (default).

#### Value

`"managed"`

### `CreateDetails`

Object passed to the `create()` function.

#### Properties

*   `index`

    `number` optional
*   `parentId`

    `string` optional

    Defaults to the Other Bookmarks folder.
*   `title`

    `string` optional
*   `url`

    `string` optional

### `FolderType`

Chrome 134+

Indicates the type of folder.

#### Enum

*   `"bookmarks-bar"`
    The folder whose contents is displayed at the top of the browser window.
*   `"other"`
    Bookmarks which are displayed in the full list of bookmarks on all platforms.
*   `"mobile"`
    Bookmarks generally available on the user's mobile devices, but modifiable by extension or in the bookmarks manager.
*   `"managed"`
    A top-level folder that may be present if the system administrator or the custodian of a supervised user has configured bookmarks.

## Properties

### `MAX_SUSTAINED_WRITE_OPERATIONS_PER_MINUTE`

Deprecated

Bookmark write operations are no longer limited by Chrome.

#### Value

`1000000`

### `MAX_WRITE_OPERATIONS_PER_HOUR`

Deprecated

Bookmark write operations are no longer limited by Chrome.

#### Value

`1000000`

## Methods

### `create()`

Promise

```javascript
chrome.bookmarks.create(
  bookmark: CreateDetails,
  callback?: function,
)
```

Creates a bookmark or folder under the specified `parentId`. If `url` is `NULL` or missing, it will be a folder.

#### Parameters

*   `bookmark`

    `CreateDetails`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result: BookmarkTreeNode) => void
    ```

    *   `result`

        `BookmarkTreeNode`

#### Returns

*   `Promise<BookmarkTreeNode>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `get()`

Promise

```javascript
chrome.bookmarks.get(
  idOrIdList: string | [string, ...string[]],
  callback?: function,
)
```

Retrieves the specified `BookmarkTreeNode`(s).

#### Parameters

*   `idOrIdList`

    `string` | `[string, ...string[]]`

    A single string-valued `id`, or an array of string-valued `id`s
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getChildren()`

Promise

```javascript
chrome.bookmarks.getChildren(
  id: string,
  callback?: function,
)
```

Retrieves the children of the specified `BookmarkTreeNode` `id`.

#### Parameters

*   `id`

    `string`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getRecent()`

Promise

```javascript
chrome.bookmarks.getRecent(
  numberOfItems: number,
  callback?: function,
)
```

Retrieves the recently added bookmarks.

#### Parameters

*   `numberOfItems`

    `number`

    The maximum number of items to return.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getSubTree()`

Promise

```javascript
chrome.bookmarks.getSubTree(
  id: string,
  callback?: function,
)
```

Retrieves part of the Bookmarks hierarchy, starting at the specified node.

#### Parameters

*   `id`

    `string`

    The ID of the root of the subtree to retrieve.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getTree()`

Promise

```javascript
chrome.bookmarks.getTree(
  callback?: function,
)
```

Retrieves the entire Bookmarks hierarchy.

#### Parameters

*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `move()`

Promise

```javascript
chrome.bookmarks.move(
  id: string,
  destination: object,
  callback?: function,
)
```

Moves the specified `BookmarkTreeNode` to the provided location.

#### Parameters

*   `id`

    `string`
*   `destination`

    `object`

    *   `index`

        `number` optional
    *   `parentId`

        `string` optional
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result: BookmarkTreeNode) => void
    ```

    *   `result`

        `BookmarkTreeNode`

#### Returns

*   `Promise<BookmarkTreeNode>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `remove()`

Promise

```javascript
chrome.bookmarks.remove(
  id: string,
  callback?: function,
)
```

Removes a bookmark or an empty bookmark folder.

#### Parameters

*   `id`

    `string`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `removeTree()`

Promise

```javascript
chrome.bookmarks.removeTree(
  id: string,
  callback?: function,
)
```

Recursively removes a bookmark folder.

#### Parameters

*   `id`

    `string`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `search()`

Promise

```javascript
chrome.bookmarks.search(
  query: string | object,
  callback?: function,
)
```

Searches for `BookmarkTreeNode`s matching the given query. Queries specified with an object produce `BookmarkTreeNode`s matching all specified properties.

#### Parameters

*   `query`

    `string` | `object`

    Either a string of words and quoted phrases that are matched against bookmark URLs and titles, or an object. If an object, the properties `query`, `url`, and `title` may be specified and bookmarks matching all specified properties will be produced.

    *   `query`

        `string` optional

        A string of words and quoted phrases that are matched against bookmark URLs and titles.
    *   `title`

        `string` optional

        The title of the bookmark; matches verbatim.
    *   `url`

        `string` optional

        The URL of the bookmark; matches verbatim. Note that folders have no URL.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (results: BookmarkTreeNode[]) => void
    ```

    *   `results`

        `BookmarkTreeNode[]`

#### Returns

*   `Promise<BookmarkTreeNode[]>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `update()`

Promise

```javascript
chrome.bookmarks.update(
  id: string,
  changes: object,
  callback?: function,
)
```

Updates the properties of a bookmark or folder. Specify only the properties that you want to change; unspecified properties will be left unchanged. Note: Currently, only `'title'` and `'url'` are supported.

#### Parameters

*   `id`

    `string`
*   `changes`

    `object`

    *   `title`

        `string` optional
    *   `url`

        `string` optional
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result: BookmarkTreeNode) => void
    ```

    *   `result`

        `BookmarkTreeNode`

#### Returns

*   `Promise<BookmarkTreeNode>`

    Chrome 90+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onChanged`

```javascript
chrome.bookmarks.onChanged.addListener(
  callback: function,
)
```

Fired when a bookmark or folder changes. Note: Currently, only `title` and `url` changes trigger this.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (id: string, changeInfo: object) => void
    ```

    *   `id`

        `string`
    *   `changeInfo`

        `object`

        *   `title`

            `string`
        *   `url`

            `string` optional

### `onChildrenReordered`

```javascript
chrome.bookmarks.onChildrenReordered.addListener(
  callback: function,
)
```

Fired when the children of a folder have changed their order due to the order being sorted in the UI. This is not called as a result of a `move()`.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (id: string, reorderInfo: object) => void
    ```

    *   `id`

        `string`
    *   `reorderInfo`

        `object`

        *   `childIds`

            `string[]`

### `onCreated`

```javascript
chrome.bookmarks.onCreated.addListener(
  callback: function,
)
```

Fired when a bookmark or folder is created.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (id: string, bookmark: BookmarkTreeNode) => void
    ```

    *   `id`

        `string`
    *   `bookmark`

        `BookmarkTreeNode`

### `onImportBegan`

```javascript
chrome.bookmarks.onImportBegan.addListener(
  callback: function,
)
```

Fired when a bookmark import session is begun. Expensive observers should ignore `onCreated` updates until `onImportEnded` is fired. Observers should still handle other notifications immediately.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    () => void
    ```

### `onImportEnded`

```javascript
chrome.bookmarks.onImportEnded.addListener(
  callback: function,
)
```

Fired when a bookmark import session is ended.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    () => void
    ```

### `onMoved`

```javascript
chrome.bookmarks.onMoved.addListener(
  callback: function,
)
```

Fired when a bookmark or folder is moved to a different parent folder.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (id: string, moveInfo: object) => void
    ```

    *   `id`

        `string`
    *   `moveInfo`

        `object`

        *   `index`

            `number`
        *   `oldIndex`

            `number`
        *   `oldParentId`

            `string`
        *   `parentId`

            `string`

### `onRemoved`

```javascript
chrome.bookmarks.onRemoved.addListener(
  callback: function,
)
```

Fired when a bookmark or folder is removed. When a folder is removed recursively, a single notification is fired for the folder, and none for its contents.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (id: string, removeInfo: object) => void
    ```

    *   `id`

        `string`
    *   `removeInfo`

        `object`

        *   `index`

            `number`
        *   `node`

            `BookmarkTreeNode`

            Chrome 48+
        *   `parentId`

            `string`

===

---
title: chrome.browsingData
url: https://developer.chrome.com/docs/extensions/reference/api/browsingData
---

# chrome.browsingData

## Description

Use the `chrome.browsingData` API to remove browsing data from a user's local profile.

## Permissions

`browsingData`

You must declare the "browsingData" permission in the extension manifest to use this API.

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "browsingData"
  ],
  ...
}
```

## Concepts and usage

The simplest use-case for this API is a a time-based mechanism for clearing a user's browsing data. Your code should provide a timestamp which indicates the historical date after which the user's browsing data should be removed. This timestamp is formatted as the number of milliseconds since the Unix epoch (which can be retrieved from a JavaScript `Date` object using the `getTime()` method).

For example, to clear all of a user's browsing data from the last week, you might write code as follows:

```javascript
var callback = function () {
  // Do something clever here once data has been removed.
};
var millisecondsPerWeek = 1000 * 60 * 60 * 24 * 7;
var oneWeekAgo = (new Date()).getTime() - millisecondsPerWeek;
chrome.browsingData.remove({
  "since": oneWeekAgo
}, {
  "appcache": true,
  "cache": true,
  "cacheStorage": true,
  "cookies": true,
  "downloads": true,
  "fileSystems": true,
  "formData": true,
  "history": true,
  "indexedDB": true,
  "localStorage": true,
  "passwords": true,
  "serviceWorkers": true,
  "webSQL": true
}, callback);
```

The `chrome.browsingData.remove()` method lets you remove various types of browsing data with a single call, and will be much faster than calling multiple more specific methods. If, however, you only want to clear one specific type of browsing data (cookies, for example), the more granular methods offer a readable alternative to a call filled with JSON.

```javascript
var callback = function () {
  // Do something clever here once data has been removed.
};
var millisecondsPerWeek = 1000 * 60 * 60 * 24 * 7;
var oneWeekAgo = (new Date()).getTime() - millisecondsPerWeek;
chrome.browsingData.removeCookies({
  "since": oneWeekAgo
}, callback);
```

If the user is syncing their data, `chrome.browsingData.remove()` may automatically rebuild the cookie for the Sync account after clearing it. This is to ensure that Sync can continue working, so that the data can be eventually deleted on the server. However the more specific `chrome.browsingData.removeCookies()` can be used to clear the cookie for the Sync account, and Sync will be paused in this case.

Important: Removing browsing data involves a good deal of heavy lifting in the background, and can take tens of seconds to complete, depending on a user's profile. You should use either the returned promise or the callback to keep your users up to date on the removal's status.

### Specific origins

To remove data for a specific origin or to exclude a set of origins from deletion, you can use the `RemovalOptions.origins` and `RemovalOptions.excludeOrigins` parameters. They can only be applied to cookies, cache, and storage (`CacheStorage`, `FileSystems`, `IndexedDB`, `LocalStorage`, `ServiceWorkers`, and `WebSQL`).

```javascript
chrome.browsingData.remove({
  "origins": ["https://www.example.com"]
}, {
  "cacheStorage": true,
  "cookies": true,
  "fileSystems": true,
  "indexedDB": true,
  "localStorage": true,
  "serviceWorkers": true,
  "webSQL": true
}, callback);
```

Important: As cookies are scoped more broadly than other types of storage, deleting cookies for an origin will delete all cookies of the registrable domain. For example, deleting data for `https://www.example.com` will delete cookies with a domain of `.example.com` as well.

### Origin types

Adding an `originTypes` property to the APIs options object lets you specify which types of origins ought to be effected. Origins are divided into three categories:

*   `unprotectedWeb` covers the general case of websites that users visit without taking any special action. If you don't specify an `originTypes`, the API defaults to removing data from unprotected web origins.
*   `protectedWeb` covers those web origins that have been installed as hosted applications. Installing Angry Birds, for example, protects the origin `https://chrome.angrybirds.com`, and removes it from the `unprotectedWeb` category. Be careful when triggering deletion of data for these origins: make sure your users know what they're getting, as this will irrevocably remove their game data. No one wants to knock tiny pig houses over more often than necessary.
*   `extension` covers origins under the `chrome-extensions:` scheme. Removing extension data is, again, something you should be very careful about.

We could adjust the previous example to remove only data from protected websites as follows:

```javascript
var callback = function () {
  // Do something clever here once data has been removed.
};
var millisecondsPerWeek = 1000 * 60 * 60 * 24 * 7;
var oneWeekAgo = (new Date()).getTime() - millisecondsPerWeek;
chrome.browsingData.remove({
  "since": oneWeekAgo,
  "originTypes": {
    "protectedWeb": true
  }
}, {
  "appcache": true,
  "cache": true,
  "cacheStorage": true,
  "cookies": true,
  "downloads": true,
  "fileSystems": true,
  "formData": true,
  "history": true,
  "indexedDB": true,
  "localStorage": true,
  "passwords": true,
  "serviceWorkers": true,
  "webSQL": true
}, callback);
```

Warning: Be careful with the `protectedWeb` and `extension` origin types. These are destructive operations that may surprise your users if they're not well-informed about what to expect when your extension removes data on their behalf.

## Examples

To try this API, install the browsingData API example from the chrome-extension-samples repository.

## Types

### DataTypeSet

A set of data types. Missing data types are interpreted as `false`.

#### Properties

*   `appcache`
    boolean optional
    Websites' appcaches.
*   `cache`
    boolean optional
    The browser's cache.
*   `cacheStorage`
    boolean optional
    Chrome 72+
    Cache storage
*   `cookies`
    boolean optional
    The browser's cookies.
*   `downloads`
    boolean optional
    The browser's download list.
*   `fileSystems`
    boolean optional
    Websites' file systems.
*   `formData`
    boolean optional
    The browser's stored form data.
*   `history`
    boolean optional
    The browser's history.
*   `indexedDB`
    boolean optional
    Websites' IndexedDB data.
*   `localStorage`
    boolean optional
    Websites' local storage data.
*   `passwords`
    boolean optional
    Stored passwords.
*   `pluginData`
    boolean optional
    Deprecated since Chrome 88
    Support for Flash has been removed. This data type will be ignored.
    Plugins' data.
*   `serverBoundCertificates`
    boolean optional
    Deprecated since Chrome 76
    Support for server-bound certificates has been removed. This data type will be ignored.
    Server-bound certificates.
*   `serviceWorkers`
    boolean optional
    Service Workers.
*   `webSQL`
    boolean optional
    Websites' WebSQL data.

### RemovalOptions

Options that determine exactly what data will be removed.

#### Properties

*   `excludeOrigins`
    string[] optional
    Chrome 74+
    When present, data for origins in this list is excluded from deletion. Can't be used together with `origins`. Only supported for cookies, storage and cache. Cookies are excluded for the whole registrable domain.
*   `originTypes`
    object optional
    An object whose properties specify which origin types ought to be cleared. If this object isn't specified, it defaults to clearing only "unprotected" origins. Please ensure that you really want to remove application data before adding 'protectedWeb' or 'extensions'.
    *   `extension`
        boolean optional
        Extensions and packaged applications a user has installed (be \_really\_ careful!).
    *   `protectedWeb`
        boolean optional
        Websites that have been installed as hosted applications (be careful!).
    *   `unprotectedWeb`
        boolean optional
        Normal websites.
*   `origins`
    [string, ...string[]] optional
    Chrome 74+
    When present, only data for origins in this list is deleted. Only supported for cookies, storage and cache. Cookies are cleared for the whole registrable domain.
*   `since`
    number optional
    Remove data accumulated on or after this date, represented in milliseconds since the epoch (accessible via the `getTime` method of the JavaScript `Date` object). If absent, defaults to 0 (which would remove all browsing data).

## Methods

### remove()

Promise

```
chrome.browsingData.remove(
  options: RemovalOptions,
  dataToRemove: DataTypeSet,
  callback?: function,
)
```

Clears various types of browsing data stored in a user's profile.

#### Parameters

*   `options`
    `RemovalOptions`
*   `dataToRemove`
    `DataTypeSet`
    The set of data types to remove.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeAppcache()

Promise

```
chrome.browsingData.removeAppcache(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' appcache data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeCache()

Promise

```
chrome.browsingData.removeCache(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's cache.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeCacheStorage()

Promise Chrome 72+

```
chrome.browsingData.removeCacheStorage(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' cache storage data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeCookies()

Promise

```
chrome.browsingData.removeCookies(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's cookies and server-bound certificates modified within a particular timeframe.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeDownloads()

Promise

```
chrome.browsingData.removeDownloads(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's list of downloaded files (not the downloaded files themselves).

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeFileSystems()

Promise

```
chrome.browsingData.removeFileSystems(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' file system data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeFormData()

Promise

```
chrome.browsingData.removeFormData(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's stored form data (autofill).

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeHistory()

Promise

```
chrome.browsingData.removeHistory(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's history.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeIndexedDB()

Promise

```
chrome.browsingData.removeIndexedDB(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' IndexedDB data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeLocalStorage()

Promise

```
chrome.browsingData.removeLocalStorage(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' local storage data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removePasswords()

Promise

```
chrome.browsingData.removePasswords(
  options: RemovalOptions,
  callback?: function,
)
```

Clears the browser's stored passwords.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removePluginData()

Promise Deprecated since Chrome 88

```
chrome.browsingData.removePluginData(
  options: RemovalOptions,
  callback?: function,
)
```

Support for Flash has been removed. This function has no effect.

Clears plugins' data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeServiceWorkers()

Promise Chrome 72+

```
chrome.browsingData.removeServiceWorkers(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' service workers.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeWebSQL()

Promise

```
chrome.browsingData.removeWebSQL(
  options: RemovalOptions,
  callback?: function,
)
```

Clears websites' WebSQL data.

#### Parameters

*   `options`
    `RemovalOptions`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### settings()

Promise

```
chrome.browsingData.settings(
  callback?: function,
)
```

Reports which types of data are currently selected in the 'Clear browsing data' settings UI. Note: some of the data types included in this API are not available in the settings UI, and some UI settings control more than one data type listed here.

#### Parameters

*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (result: object) => void
    ```
    *   `result`
        object
        *   `dataRemovalPermitted`
            `DataTypeSet`
            All of the types will be present in the result, with values of `true` if they are permitted to be removed (e.g., by enterprise policy) and `false` if not.
        *   `dataToRemove`
            `DataTypeSet`
            All of the types will be present in the result, with values of `true` if they are both selected to be removed and permitted to be removed, otherwise `false`.
        *   `options`
            `RemovalOptions`

#### Returns

*   Promise&lt;object&gt;
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.certificateProvider
url: https://developer.chrome.com/docs/extensions/reference/api/certificateProvider
---

# chrome.certificateProvider

Important: This API works only on ChromeOS.

## Description

Use this API to expose certificates to the platform which can use these certificates for TLS authentications.

## Permissions

`certificateProvider`

## Availability

Chrome 46+ ChromeOS only

## Concepts and usage

Typical usage of this API to expose client certificates to ChromeOS follows these steps:

*   The Extension registers for the events `onCertificatesUpdateRequested` and `onSignatureRequested`.
*   The Extension calls `setCertificates()` to provide the initial list of certificates after the initialization.
*   The Extension monitors the changes in the list of available certificates and calls `setCertificates()` to notify the browser about every such change.
*   During a TLS handshake, the browser receives a client certificate request. With an `onCertificatesUpdateRequested` event, the browser asks the Extension to report all certificates that it currently provides.
*   The Extension reports back with the currently available certificates, using the `setCertificates()` method.
*   The browser matches all available certificates with the client certificate request from the remote host. The matches are presented to the user in a selection dialog.
*   The user can select a certificate and thereby approve the authentication or abort the authentication.

Certificate selection dialog.

*   If the user aborts the authentication or no certificate matched the request, the TLS client authentication is aborted.
*   Otherwise, if the user approves the authentication with a certificate provided by this Extension, the browser requests the Extension to sign the data to continue the TLS handshake. The request is sent as a `onSignatureRequested` event.
*   This event contains input data, declares which algorithm has to be used to generate the signature, and refers to one of the certificates that were reported by this Extension. The Extension must create a signature for the given data using the private key associated with the referenced certificate. Creating the signature might require prepending a `DigestInfo` and padding the result before the actual signing.
*   The Extension sends back the signature to the browser using the `reportSignature()` method. If the signature couldn't be calculated, the method has to be called without signature.
*   If the signature was provided, the browser completes the TLS handshake.

The actual sequence of steps can be different. For example, the user will not be asked to select a certificate if the enterprise policy to automatically select a certificate is used (see `AutoSelectCertificateForUrls` and Chrome policies for users).

In the Extension, this can look similar to the following snippet:

```javascript
function collectAvailableCertificates() {
  // Return all certificates that this Extension can currently provide.
  // For example:
  return [{
    certificateChain: [new Uint8Array(...)],
    supportedAlgorithms: ['RSASSA_PKCS1_v1_5_SHA256']
  }];
}

// The Extension calls this function every time the currently available list of
// certificates changes, and also once after the Extension's initialization.
function onAvailableCertificatesChanged() {
  chrome.certificateProvider.setCertificates({
    clientCertificates: collectAvailableCertificates()
  });
}

function handleCertificatesUpdateRequest(request) {
  // Report the currently available certificates as a response to the request
  // event. This is important for supporting the case when the Extension is
  // unable to detect the changes proactively.
  chrome.certificateProvider.setCertificates({
    certificatesRequestId: request.certificatesRequestId,
    clientCertificates: collectAvailableCertificates()
  });
}

// Returns a private key handle for the given DER-encoded certificate.
// |certificate| is an ArrayBuffer.
function getPrivateKeyHandle(certificate) {/*...*/}

// Digests and signs |input| with the given private key. |input| is an
// ArrayBuffer. |algorithm| is an Algorithm.
// Returns the signature as ArrayBuffer.
function signUnhashedData(privateKey, input, algorithm) {/*...*/}

function handleSignatureRequest(request) {
  // Look up the handle to the private key of |request.certificate|.
  const key = getPrivateKeyHandle(request.certificate);
  if (!key) {
    // Handle if the key isn't available.
    console.error('Key for requested certificate no available.');
    // Abort the request by reporting the error to the API.
    chrome.certificateProvider.reportSignature({
      signRequestId: request.signRequestId,
      error: 'GENERAL_ERROR'
    });
    return;
  }
  const signature = signUnhashedData(key, request.input, request.algorithm);
  chrome.certificateProvider.reportSignature({
    signRequestId: request.signRequestId,
    signature: signature
  });
}

chrome.certificateProvider.onCertificatesUpdateRequested.addListener(
  handleCertificatesUpdateRequest);
chrome.certificateProvider.onSignatureRequested.addListener(
  handleSignatureRequest);
```

## Types

### `Algorithm`

Chrome 86+
Types of supported cryptographic signature algorithms.

#### Enum

`"RSASSA_PKCS1_v1_5_MD5_SHA1"` Specifies the RSASSA PKCS#1 v1.5 signature algorithm with the MD5-SHA-1 hashing. The extension must not prepend a `DigestInfo` prefix but only add PKCS#1 padding. This algorithm is deprecated and will never be requested by Chrome as of version 109.
`"RSASSA_PKCS1_v1_5_SHA1"` Specifies the RSASSA PKCS#1 v1.5 signature algorithm with the SHA-1 hash function.
`"RSASSA_PKCS1_v1_5_SHA256"` Specifies the RSASSA PKCS#1 v1.5 signature algorithm with the SHA-256 hashing function.
`"RSASSA_PKCS1_v1_5_SHA384"` Specifies the RSASSA PKCS#1 v1.5 signature algorithm with the SHA-384 hashing function.
`"RSASSA_PKCS1_v1_5_SHA512"` Specifies the RSASSA PKCS#1 v1.5 signature algorithm with the SHA-512 hashing function.
`"RSASSA_PSS_SHA256"` Specifies the RSASSA PSS signature algorithm with the SHA-256 hashing function, MGF1 mask generation function and the salt of the same size as the hash.
`"RSASSA_PSS_SHA384"` Specifies the RSASSA PSS signature algorithm with the SHA-384 hashing function, MGF1 mask generation function and the salt of the same size as the hash.
`"RSASSA_PSS_SHA512"` Specifies the RSASSA PSS signature algorithm with the SHA-512 hashing function, MGF1 mask generation function and the salt of the same size as the hash.

### `CertificateInfo`

#### Properties

*   `certificate`
    `ArrayBuffer`
    Must be the DER encoding of a X.509 certificate. Currently, only certificates of RSA keys are supported.
*   `supportedHashes`
    `Hash[]`
    Must be set to all hashes supported for this certificate. This extension will only be asked for signatures of digests calculated with one of these hash algorithms. This should be in order of decreasing hash preference.

### `CertificatesUpdateRequest`

Chrome 86+

#### Properties

*   `certificatesRequestId`
    `number`
    Request identifier to be passed to `setCertificates`.

### `ClientCertificateInfo`

Chrome 86+

#### Properties

*   `certificateChain`
    `ArrayBuffer[]`
    The array must contain the DER encoding of the X.509 client certificate as its first element.
    This must include exactly one certificate.
*   `supportedAlgorithms`
    `Algorithm[]`
    All algorithms supported for this certificate. The extension will only be asked for signatures using one of these algorithms.

### `Error`

Chrome 86+
Types of errors that the extension can report.

#### Value

`"GENERAL_ERROR"`

### `Hash`

Deprecated. Replaced by `Algorithm`.

#### Enum

`"MD5_SHA1"` Specifies the MD5 and SHA1 hashing algorithms.
`"SHA1"` Specifies the SHA1 hashing algorithm.
`"SHA256"` Specifies the SHA256 hashing algorithm.
`"SHA384"` Specifies the SHA384 hashing algorithm.
`"SHA512"` Specifies the SHA512 hashing algorithm.

### `PinRequestErrorType`

Chrome 57+
The types of errors that can be presented to the user through the `requestPin` function.

#### Enum

`"INVALID_PIN"` Specifies the PIN is invalid.
`"INVALID_PUK"` Specifies the PUK is invalid.
`"MAX_ATTEMPTS_EXCEEDED"` Specifies the maximum attempt number has been exceeded.
`"UNKNOWN_ERROR"` Specifies that the error cannot be represented by the above types.

### `PinRequestType`

Chrome 57+
The type of code being requested by the extension with `requestPin` function.

#### Enum

`"PIN"` Specifies the requested code is a PIN.
`"PUK"` Specifies the requested code is a PUK.

### `PinResponseDetails`

Chrome 57+

#### Properties

*   `userInput`
    `string` optional
    The code provided by the user. Empty if user closed the dialog or some other error occurred.

### `ReportSignatureDetails`

Chrome 86+

#### Properties

*   `error`
    `"GENERAL_ERROR"` optional
    Error that occurred while generating the signature, if any.
*   `signRequestId`
    `number`
    Request identifier that was received via the `onSignatureRequested` event.
*   `signature`
    `ArrayBuffer` optional
    The signature, if successfully generated.

### `RequestPinDetails`

Chrome 57+

#### Properties

*   `attemptsLeft`
    `number` optional
    The number of attempts left. This is provided so that any UI can present this information to the user. Chrome is not expected to enforce this, instead `stopPinRequest` should be called by the extension with `errorType = MAX_ATTEMPTS_EXCEEDED` when the number of pin requests is exceeded.
*   `errorType`
    `PinRequestErrorType` optional
    The error template displayed to the user. This should be set if the previous request failed, to notify the user of the failure reason.
*   `requestType`
    `PinRequestType` optional
    The type of code requested. Default is PIN.
*   `signRequestId`
    `number`
    The ID given by Chrome in `SignRequest`.

### `SetCertificatesDetails`

Chrome 86+

#### Properties

*   `certificatesRequestId`
    `number` optional
    When called in response to `onCertificatesUpdateRequested`, should contain the received `certificatesRequestId` value. Otherwise, should be unset.
*   `clientCertificates`
    `ClientCertificateInfo[]`
    List of currently available client certificates.
*   `error`
    `"GENERAL_ERROR"` optional
    Error that occurred while extracting the certificates, if any. This error will be surfaced to the user when appropriate.

### `SignatureRequest`

Chrome 86+

#### Properties

*   `algorithm`
    `Algorithm`
    Signature algorithm to be used.
*   `certificate`
    `ArrayBuffer`
    The DER encoding of a X.509 certificate. The extension must sign `input` using the associated private key.
*   `input`
    `ArrayBuffer`
    Data to be signed. Note that the data is not hashed.
*   `signRequestId`
    `number`
    Request identifier to be passed to `reportSignature`.

### `SignRequest`

#### Properties

*   `certificate`
    `ArrayBuffer`
    The DER encoding of a X.509 certificate. The extension must sign `digest` using the associated private key.
*   `digest`
    `ArrayBuffer`
    The digest that must be signed.
*   `hash`
    `Hash`
    Refers to the hash algorithm that was used to create `digest`.
*   `signRequestId`
    `number`
    Chrome 57+
    The unique ID to be used by the extension should it need to call a method that requires it, e.g. `requestPin`.

### `StopPinRequestDetails`

Chrome 57+

#### Properties

*   `errorType`
    `PinRequestErrorType` optional
    The error template. If present it is displayed to user. Intended to contain the reason for stopping the flow if it was caused by an error, e.g. `MAX_ATTEMPTS_EXCEEDED`.
*   `signRequestId`
    `number`
    The ID given by Chrome in `SignRequest`.

## Methods

### `reportSignature()`

Promise Chrome 86+

```javascript
chrome.certificateProvider.reportSignature(
  details: ReportSignatureDetails,
  callback?: function,
)
```

Should be called as a response to `onSignatureRequested`.
The extension must eventually call this function for every `onSignatureRequested` event; the API implementation will stop waiting for this call after some time and respond with a timeout error when this function is called.

#### Parameters

*   `details`
    `ReportSignatureDetails`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `requestPin()`

Promise Chrome 57+

```javascript
chrome.certificateProvider.requestPin(
  details: RequestPinDetails,
  callback?: function,
)
```

Requests the PIN from the user. Only one ongoing request at a time is allowed. The requests issued while another flow is ongoing are rejected. It's the extension's responsibility to try again later if another flow is in progress.

#### Parameters

*   `details`
    `RequestPinDetails`
    Contains the details about the requested dialog.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (details?: PinResponseDetails) => void
    ```
    *   `details`
        `PinResponseDetails` optional

#### Returns

*   `Promise<PinResponseDetails | undefined>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setCertificates()`

Promise Chrome 86+

```javascript
chrome.certificateProvider.setCertificates(
  details: SetCertificatesDetails,
  callback?: function,
)
```

Sets a list of certificates to use in the browser.
The extension should call this function after initialization and on every change in the set of currently available certificates. The extension should also call this function in response to `onCertificatesUpdateRequested` every time this event is received.

#### Parameters

*   `details`
    `SetCertificatesDetails`
    The certificates to set. Invalid certificates will be ignored.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `stopPinRequest()`

Promise Chrome 57+

```javascript
chrome.certificateProvider.stopPinRequest(
  details: StopPinRequestDetails,
  callback?: function,
)
```

Stops the pin request started by the `requestPin` function.

#### Parameters

*   `details`
    `StopPinRequestDetails`
    Contains the details about the reason for stopping the request flow.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onCertificatesUpdateRequested`

Chrome 86+

```javascript
chrome.certificateProvider.onCertificatesUpdateRequested.addListener(
  callback: function,
)
```

This event fires if the certificates set via `setCertificates` are insufficient or the browser requests updated information. The extension must call `setCertificates` with the updated list of certificates and the received `certificatesRequestId`.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (request: CertificatesUpdateRequest) => void
    ```
    *   `request`
        `CertificatesUpdateRequest`

### `onSignatureRequested`

Chrome 86+

```javascript
chrome.certificateProvider.onSignatureRequested.addListener(
  callback: function,
)
```

This event fires every time the browser needs to sign a message using a certificate provided by this extension via `setCertificates`.
The extension must sign the input data from `request` using the appropriate algorithm and private key and return it by calling `reportSignature` with the received `signRequestId`.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (request: SignatureRequest) => void
    ```
    *   `request`
        `SignatureRequest`

===

---
title: chrome.commands
url: https://developer.chrome.com/docs/extensions/reference/api/commands
---

# chrome.commands

## Description

Use the `commands` API to add keyboard shortcuts that trigger actions in your extension, for example, an action to open the browser action or send a command to the extension.

## Manifest

The following keys must be declared in the manifest to use this API.

`"commands"`

## Concepts and usage

The Commands API allows extension developers to define specific commands, and bind them to a default key combination. Each command an extension accepts must be declared as properties of the `"commands"` object in the extension's manifest.

The property key is used as the command's name. Command objects can take two properties.

`suggested_key`
:   An optional property that declares default keyboard shortcuts for the command. If omitted, the command will be unbound. This property can either take a string or an object value.
    *   A string value specifies the default keyboard shortcut that should be used across all platforms.
    *   An object value allows the extension developer to customize the keyboard shortcut for each platform. When providing platform-specific shortcuts, valid object properties are `default`, `chromeos`, `linux`, `mac`, and `windows`.
    See Key combination requirements for additional details.

`description`
:   A string used to provide the user with a short description of the command's purpose. This string appears in extension keyboard shortcut management UI. Descriptions are required for standard commands, but are ignored for Action commands.

An extension can have many commands, but may specify at most four suggested keyboard shortcuts. The user can manually add more shortcuts from the `chrome://extensions/shortcuts` dialog.

### Supported Keys

The following keys are usable command shortcuts. Key definitions are case sensitive. Attempting to load an extension with an incorrectly cased key will result in a manifest parse error at installation time.

Alpha keys
:   `A` ... `Z`

Numeric keys
:   `0` ... `9`

Standard key strings
:   General鈥揱Comma`, `Period`, `Home`, `End`, `PageUp`, `PageDown`, `Space`, `Insert`, `Delete`
:   Arrow keys鈥揱Up`, `Down`, `Left`, `Right`
:   Media Keys鈥揱MediaNextTrack`, `MediaPlayPause`, `MediaPrevTrack`, `MediaStop`

Modifier key strings
:   `Ctrl`, `Alt`, `Shift`, `MacCtrl` (macOS only), `Command` (macOS only), `Search` (ChromeOS only)

### Key combination requirements

*   Extension command shortcuts must include either `Ctrl` or `Alt`.
    *   Modifiers cannot be used in combination with Media Keys.
    *   On many macOS keyboards, `Alt` refers to the Option key.
    *   On macOS, `Command` or `MacCtrl` can also be used in place of `Ctrl` or `Alt` (see next bullet point).
*   On macOS `Ctrl` is automatically converted into `Command`.
    *   `Command` can also be used in the `"mac"` shortcut to explicitly refer to the `Command` key.
    *   To use the `Control` key on macOS, replace `Ctrl` with `MacCtrl` when defining the `"mac"` shortcut.
    *   Using `MacCtrl` in the combination for another platform will cause a validation error and prevent the extension from being installed.
*   `Shift` is an optional modifier on all platforms.
*   `Search` is an optional modifier exclusive to ChromeOS.
*   Certain operating system and Chrome shortcuts (e.g. window management) always take priority over Extension command shortcuts and cannot be overridden.

Note: Key combinations that involve `Ctrl`+`Alt` are not permitted in order to avoid conflicts with the `AltGr` key.

### Handle command events

manifest.json:

```json
{
  "name": "My extension",
  ...
  "commands": {
    "run-foo": {
      "suggested_key": {
        "default": "Ctrl+Shift+Y",
        "mac": "Command+Shift+Y"
      },
      "description": "Run \"foo\" on the current page."
    },
    "_execute_action": {
      "suggested_key": {
        "windows": "Ctrl+Shift+Y",
        "mac": "Command+Shift+Y",
        "chromeos": "Ctrl+Shift+U",
        "linux": "Ctrl+Shift+J"
      }
    }
  },
  ...
}
```

In your service worker, you can bind a handler to each of the commands defined in the manifest using `onCommand.addListener`. For example:

service-worker.js:

```javascript
chrome.commands.onCommand.addListener((command) => {
  console.log(`Command: ${command}`);
});
```

### Action commands

The `_execute_action` (Manifest V3), `_execute_browser_action` (Manifest V2), and `_execute_page_action` (Manifest V2) commands are reserved for the action of trigger your action, browser action, or page action respectively. These commands don't dispatch `command.onCommand` events like standard commands.

If you need to take action based on your popup opening, consider listening for a `DOMContentLoaded` event inside your popup's JavaScript.

### Scope

By default, commands are scoped to the Chrome browser. This means that when the browser does not have focus, command shortcuts are inactive. Beginning in Chrome 35, extension developers can optionally mark a command as `"global"`. Global commands also work while Chrome does not have focus.

Note: ChromeOS does not support global commands.

Keyboard shortcut suggestions for global commands are limited to `Ctrl`+`Shift`+`[0..9]`. This is a protective measure to minimize the risk of overriding shortcuts in other applications since if, for example, `Alt`+`P` were to be allowed as global, the keyboard shortcut for opening a print dialog might not work in other applications.

End users are free to remap global commands to their preferred key combination using the UI exposed at `chrome://extensions/shortcuts`.

Example:

manifest.json:

```json
{
  "name": "My extension",
  ...
  "commands": {
    "toggle-feature-foo": {
      "suggested_key": {
        "default": "Ctrl+Shift+5"
      },
      "description": "Toggle feature foo",
      "global": true
    }
  },
  ...
}
```

## Examples

The following examples flex the core functionality of the Commands API.

### Basic command

Commands allow extensions to map logic to keyboard shortcuts that can be invoked by the user. At its most basic, a command only requires a command declaration in the extension's manifest and a listener registration as shown in the following example.

manifest.json:

```json
{
  "name": "Command demo - basic",
  "version": "1.0",
  "manifest_version": 3,
  "background": {
    "service_worker": "service-worker.js"
  },
  "commands": {
    "inject-script": {
      "suggested_key": "Ctrl+Shift+Y",
      "description": "Inject a script on the page"
    }
  }
}
```

service-worker.js:

```javascript
chrome.commands.onCommand.addListener((command) => {
  console.log(`Command "${command}" triggered`);
});
```

### Action command

As described in the Concepts and usage section, you can also map a command to an extension's action. The following example injects a content script that shows an alert on the current page when the user either clicks the extension's action or triggers the keyboard shortcut.

manifest.json:

```json
{
  "name": "Commands demo - action invocation",
  "version": "1.0",
  "manifest_version": 3,
  "background": {
    "service_worker": "service-worker.js"
  },
  "permissions": ["activeTab", "scripting"],
  "action": {},
  "commands": {
    "_execute_action": {
      "suggested_key": {
        "default": "Ctrl+U",
        "mac": "Command+U"
      }
    }
  }
}
```

service-worker.js:

```javascript
chrome.action.onClicked.addListener((tab) => {
  chrome.scripting.executeScript({
    target: {tabId: tab.id},
    func: contentScriptFunc,
    args: ['action'],
  });
});

function contentScriptFunc(name) {
  alert(`"${name}" executed`);
}

// This callback WILL NOT be called for "_execute_action"
chrome.commands.onCommand.addListener((command) => {
  console.log(`Command "${command}" called`);
});
```

### Verify commands registered

If an extension attempts to register a shortcut that is already used by another extension, the second extension's shortcut won't register as expected. You can provide a more robust end user experience by anticipating this possibility and checking for collisions at install time.

service-worker.js:

```javascript
chrome.runtime.onInstalled.addListener((details) => {
  if (details.reason === chrome.runtime.OnInstalledReason.INSTALL) {
    checkCommandShortcuts();
  }
});

// Only use this function during the initial install phase. After
// installation the user may have intentionally unassigned commands.
function checkCommandShortcuts() {
  chrome.commands.getAll((commands) => {
    let missingShortcuts = [];
    for (let {name, shortcut} of commands) {
      if (shortcut === '') {
        missingShortcuts.push(name);
      }
    }
    if (missingShortcuts.length > 0) {
      // Update the extension UI to inform the user that one or more
      // commands are currently unassigned.
    }
  });
}
```

## Types

### `Command`

#### Properties

*   `description`
    `string` optional
    The Extension Command description
*   `name`
    `string` optional
    The name of the Extension Command
*   `shortcut`
    `string` optional
    The shortcut active for this command, or blank if not active.

## Methods

### `getAll()`

Promise

```javascript
chrome.commands.getAll(
  callback?: function,
)
```

Returns all the registered extension commands for this extension and their shortcut (if active). Before Chrome 110, this command did not return `_execute_action`.

#### Parameters

*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    (commands: Command[]) => void
    ```
    *   `commands`
        `Command[]`

#### Returns

*   `Promise<Command[]>`
    Chrome 96+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onCommand`

```javascript
chrome.commands.onCommand.addListener(
  callback: function,
)
```

Fired when a registered command is activated using a keyboard shortcut.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (command: string, tab?: tabs.Tab) => void
    ```
    *   `command`
        `string`
    *   `tab`
        `tabs.Tab` optional

===

---
title: chrome.contentSettings
url: https://developer.chrome.com/docs/extensions/reference/api/contentSettings
---

# chrome.contentSettings

## Description

Use the `chrome.contentSettings` API to change settings that control whether websites can use features such as cookies, JavaScript, and plugins. More generally speaking, content settings allow you to customize Chrome's behavior on a per-site basis instead of globally.

## Permissions

`contentSettings`

You must declare the `"contentSettings"` permission in your extension's manifest to use the API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "contentSettings"
  ],
  ...
}
```

## Concepts and usage

### Content setting patterns

You can use patterns to specify the websites that each content setting affects. For example, `https://*.youtube.com/*` specifies `youtube.com` and all of its subdomains. The syntax for content setting patterns is the same as for match patterns, with a few differences:

*   For `http`, `https`, and `ftp` URLs, the path must be a wildcard (`/*`). For `file` URLs, the path must be completely specified and must not contain wildcards.
*   In contrast to match patterns, content setting patterns can specify a port number. If a port number is specified, the pattern only matches websites with that port. If no port number is specified, the pattern matches all ports.

### Pattern precedence

When more than one content setting rule applies for a given site, the rule with the more specific pattern takes precedence.

For example, the following patterns are ordered by precedence:

1.  `https://www.example.com/*`
2.  `https://*.example.com/*` (matching `example.com` and all subdomains)
3.  `<all_urls>` (matching every URL)

Three kinds of wildcards affect how specific a pattern is:

*   Wildcards in the port (for example `https://www.example.com:*/*`)
*   Wildcards in the scheme (for example `*://www.example.com:123/*`)
*   Wildcards in the hostname (for example `https://*.example.com:123/*`)

If a pattern is more specific than another pattern in one part but less specific in another part, the different parts are checked in the following order: hostname, scheme, port. For example, the following patterns are ordered by precedence:

1.  `https://www.example.com:*/*` Specifies the hostname and scheme.
2.  `*:/www.example.com:123/*` Not as high, because although it specifies the hostname, it doesn't specify the scheme.
3.  `https://*.example.com:123/*` Lower because although it specifies the port and scheme, it has a wildcard in the hostname.

### Primary and secondary patterns

The URL taken into account when deciding which content setting to apply depends on the content type. For example, for `contentSettings.notifications` settings are based on the URL shown in the omnibox. This URL is called the "primary" URL.

Some content types can take additional URLs into account. For example, whether a site is allowed to set a `contentSettings.cookies` is decided based on the URL of the HTTP request (which is the primary URL in this case) as well as the URL shown in the omnibox (which is called the "secondary" URL).

If multiple rules have primary and secondary patterns, the rule with the more specific primary pattern takes precedence. If there multiple rules have the same primary pattern, the rule with the more specific secondary pattern takes precedence. For example, the following list of primary/secondary pattern pairs is ordered by precedence:

| Precedence | Primary pattern             | Secondary pattern           |
| :--------- | :-------------------------- | :-------------------------- |
| 1          | `https://www.moose.com/*`,  | `https://www.wombat.com/*`  |
| 2          | `https://www.moose.com/*`,  | `<all_urls>`                |
| 3          | `<all_urls>`,               | `https://www.wombat.com/*`  |
| 4          | `<all_urls>`,               | `<all_urls>`                |

Secondary patterns are not supported for the `images` content setting.

### Resource identifiers

Resource identifiers allow you to specify content settings for specific subtypes of a content type. Currently, the only content type that supports resource identifiers is `contentSettings.plugins`, where a resource identifier identifies a specific plugin. When applying content settings, first the settings for the specific plugin are checked. If there are no settings found for the specific plugin, the general content settings for plugins are checked.

For example, if a content setting rule has the resource identifier `adobe-flash-player` and the pattern `<all_urls>`, it takes precedence over a rule without a resource identifier and the pattern `https://www.example.com/*`, even if that pattern is more specific.

You can get a list of resource identifiers for a content type by calling the `contentSettings.ContentSetting.getResourceIdentifiers()` method. The returned list can change with the set of installed plugins on the user's machine, but Chrome tries to keep the identifiers stable across plugin updates.

## Examples

To try this API, install the contentSettings API example from the chrome-extension-samples repository.

## Types

### `AutoVerifyContentSetting`

Chrome 113+

#### Enum

`"allow"`
`"block"`

### `CameraContentSetting`

Chrome 46+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `ClipboardContentSetting`

Chrome 121+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `ContentSetting`

#### Properties

*   `clear`
    `void`
    Promise
    Clear all content setting rules set by this extension.
    The `clear` function looks like:
    ```javascript
    (details: object, callback?: function) => {...}
    ```
    *   `details`
        `object`
        *   `scope`
            `Scope` optional
            Where to clear the setting (default: `regular`).
    *   `callback`
        `function` optional
        The callback parameter looks like:
        ```javascript
        () => void
        ```
    *   returns
        `Promise<void>`
        Chrome 96+
        Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
*   `get`
    `void`
    Promise
    Gets the current content setting for a given pair of URLs.
    The `get` function looks like:
    ```javascript
    (details: object, callback?: function) => {...}
    ```
    *   `details`
        `object`
        *   `incognito`
            `boolean` optional
            Whether to check the content settings for an incognito session. (default `false`)
        *   `primaryUrl`
            `string`
            The primary URL for which the content setting should be retrieved. Note that the meaning of a primary URL depends on the content type.
        *   `resourceIdentifier`
            `ResourceIdentifier` optional
            A more specific identifier of the type of content for which the settings should be retrieved.
        *   `secondaryUrl`
            `string` optional
            The secondary URL for which the content setting should be retrieved. Defaults to the primary URL. Note that the meaning of a secondary URL depends on the content type, and not all content types use secondary URLs.
    *   `callback`
        `function` optional
        The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
        *   `details`
            `object`
            *   `setting`
                `T`
                The content setting. See the description of the individual `ContentSetting` objects for the possible values.
    *   returns
        `Promise<object>`
        Chrome 96+
        Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
*   `getResourceIdentifiers`
    `void`
    Promise
    The `getResourceIdentifiers` function looks like:
    ```javascript
    (callback?: function) => {...}
    ```
    *   `callback`
        `function` optional
        The callback parameter looks like:
        ```javascript
        (resourceIdentifiers?: ResourceIdentifier[]) => void
        ```
        *   `resourceIdentifiers`
            `ResourceIdentifier[]` optional
            A list of resource identifiers for this content type, or `undefined` if this content type does not use resource identifiers.
    *   returns
        `Promise<ResourceIdentifier[]>`
        Chrome 96+
        Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
*   `set`
    `void`
    Promise
    Applies a new content setting rule.
    The `set` function looks like:
    ```javascript
    (details: object, callback?: function) => {...}
    ```
    *   `details`
        `object`
        *   `primaryPattern`
            `string`
            The pattern for the primary URL. For details on the format of a pattern, see Content Setting Patterns.
        *   `resourceIdentifier`
            `ResourceIdentifier` optional
            The resource identifier for the content type.
        *   `scope`
            `Scope` optional
            Where to set the setting (default: `regular`).
        *   `secondaryPattern`
            `string` optional
            The pattern for the secondary URL. Defaults to matching all URLs. For details on the format of a pattern, see Content Setting Patterns.
        *   `setting`
            `any`
            The setting applied by this rule. See the description of the individual `ContentSetting` objects for the possible values.
    *   `callback`
        `function` optional
        The callback parameter looks like:
        ```javascript
        () => void
        ```
    *   returns
        `Promise<void>`
        Chrome 96+
        Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `CookiesContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`
`"session_only"`

### `FullscreenContentSetting`

Chrome 44+

#### Value

`"allow"`

### `ImagesContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`

### `JavascriptContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`

### `LocationContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `MicrophoneContentSetting`

Chrome 46+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `MouselockContentSetting`

Chrome 44+

#### Value

`"allow"`

### `MultipleAutomaticDownloadsContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `NotificationsContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`
`"ask"`

### `PluginsContentSetting`

Chrome 44+

#### Value

`"block"`

### `PopupsContentSetting`

Chrome 44+

#### Enum

`"allow"`
`"block"`

### `PpapiBrokerContentSetting`

Chrome 44+

#### Value

`"block"`

### `ResourceIdentifier`

The only content type using resource identifiers is `contentSettings.plugins`. For more information, see Resource Identifiers.

#### Properties

*   `description`
    `string` optional
    A human readable description of the resource.
*   `id`
    `string`
    The resource identifier for the given content type.

### `Scope`

Chrome 44+
The scope of the `ContentSetting`. One of `regular`: setting for regular profile (which is inherited by the incognito profile if not overridden elsewhere), `incognito_session_only`: setting for incognito profile that can only be set during an incognito session and is deleted when the incognito session ends (overrides regular settings).

#### Enum

`"regular"`
`"incognito_session_only"`

## Properties

### `automaticDownloads`

Whether to allow sites to download multiple files automatically. One of `allow`: Allow sites to download multiple files automatically, `block`: Don't allow sites to download multiple files automatically, `ask`: Ask when a site wants to download files automatically after the first file. Default is `ask`. The primary URL is the URL of the top-level frame. The secondary URL is not used.

#### Type

`ContentSetting<MultipleAutomaticDownloadsContentSetting>`

### `autoVerify`

Chrome 113+
Whether to allow sites to use the Private State Tokens API. One of `allow`: Allow sites to use the Private State Tokens API, `block`: Block sites from using the Private State Tokens API. Default is `allow`. When calling `set()`, the primary URL pattern must be `<all_urls>`. The secondary URL is not used.

#### Type

`ContentSetting<AutoVerifyContentSetting>`

### `camera`

Chrome 46+
Whether to allow sites to access the camera. One of `allow`: Allow sites to access the camera, `block`: Don't allow sites to access the camera, `ask`: Ask when a site wants to access the camera. Default is `ask`. The primary URL is the URL of the document which requested camera access. The secondary URL is not used. NOTE: The `'allow'` setting is not valid if both patterns are `'<all_urls>'`.

#### Type

`ContentSetting<CameraContentSetting>`

### `clipboard`

Chrome 121+
Whether to allow sites to access the clipboard via advanced capabilities of the Async Clipboard API. "Advanced" capabilities include anything besides writing built-in formats after a user gesture, i.e. the ability to read, the ability to write custom formats, and the ability to write without a user gesture. One of `allow`: Allow sites to use advanced clipboard capabilities, `block`: Don't allow sites to use advanced clipboard capabilties, `ask`: Ask when a site wants to use advanced clipboard capabilities. Default is `ask`. The primary URL is the URL of the document which requested clipboard access. The secondary URL is not used.

#### Type

`ContentSetting<ClipboardContentSetting>`

### `cookies`

Whether to allow cookies and other local data to be set by websites. One of `allow`: Accept cookies, `block`: Block cookies, `session_only`: Accept cookies only for the current session. Default is `allow`. The primary URL is the URL representing the cookie origin. The secondary URL is the URL of the top-level frame.

#### Type

`ContentSetting<CookiesContentSetting>`

### `fullscreen`

Deprecated. No longer has any effect. Fullscreen permission is now automatically granted for all sites. Value is always `allow`.

#### Type

`ContentSetting<FullscreenContentSetting>`

### `images`

Whether to show images. One of `allow`: Show images, `block`: Don't show images. Default is `allow`. The primary URL is the URL of the top-level frame. The secondary URL is the URL of the image.

#### Type

`ContentSetting<ImagesContentSetting>`

### `javascript`

Whether to run JavaScript. One of `allow`: Run JavaScript, `block`: Don't run JavaScript. Default is `allow`. The primary URL is the URL of the top-level frame. The secondary URL is not used.

#### Type

`ContentSetting<JavascriptContentSetting>`

### `location`

Whether to allow Geolocation. One of `allow`: Allow sites to track your physical location, `block`: Don't allow sites to track your physical location, `ask`: Ask before allowing sites to track your physical location. Default is `ask`. The primary URL is the URL of the document which requested location data. The secondary URL is the URL of the top-level frame (which may or may not differ from the requesting URL).

#### Type

`ContentSetting<LocationContentSetting>`

### `microphone`

Chrome 46+
Whether to allow sites to access the microphone. One of `allow`: Allow sites to access the microphone, `block`: Don't allow sites to access the microphone, `ask`: Ask when a site wants to access the microphone. Default is `ask`. The primary URL is the URL of the document which requested microphone access. The secondary URL is not used. NOTE: The `'allow'` setting is not valid if both patterns are `'<all_urls>'`.

#### Type

`ContentSetting<MicrophoneContentSetting>`

### `mouselock`

Deprecated. No longer has any effect. Mouse lock permission is now automatically granted for all sites. Value is always `allow`.

#### Type

`ContentSetting<MouselockContentSetting>`

### `notifications`

Whether to allow sites to show desktop notifications. One of `allow`: Allow sites to show desktop notifications, `block`: Don't allow sites to show desktop notifications, `ask`: Ask when a site wants to show desktop notifications. Default is `ask`. The primary URL is the URL of the document which wants to show the notification. The secondary URL is not used.

#### Type

`ContentSetting<NotificationsContentSetting>`

### `plugins`

Deprecated. With Flash support removed in Chrome 88, this permission no longer has any effect. Value is always `block`. Calls to `set()` and `clear()` will be ignored.

#### Type

`ContentSetting<PluginsContentSetting>`

### `popups`

Whether to allow sites to show pop-ups. One of `allow`: Allow sites to show pop-ups, `block`: Don't allow sites to show pop-ups. Default is `block`. The primary URL is the URL of the top-level frame. The secondary URL is not used.

#### Type

`ContentSetting<PopupsContentSetting>`

### `unsandboxedPlugins`

Deprecated. Previously, controlled whether to allow sites to run plugins unsandboxed, however, with the Flash broker process removed in Chrome 88, this permission no longer has any effect. Value is always `block`. Calls to `set()` and `clear()` will be ignored.

#### Type

`ContentSetting<PpapiBrokerContentSetting>`

===

---
title: chrome.contextMenus
url: https://developer.chrome.com/docs/extensions/reference/api/contextMenus
---

# chrome.contextMenus

## Description

Use the `chrome.contextMenus` API to add items to Google Chrome's context menu. You can choose what types of objects your context menu additions apply to, such as images, hyperlinks, and pages.

## Permissions

`contextMenus`

You must declare the `"contextMenus"` permission in your extension's manifest to use the API. Also, you should specify a 16 by 16-pixel icon for display next to your menu item. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "contextMenus"
  ],
  "icons": {
    "16": "icon-bitty.png",
    "48": "icon-small.png",
    "128": "icon-large.png"
  },
  ...
}
```

## Concepts and usage

Context menu items can appear in any document (or frame within a document), even those with `file://` or `chrome://` URLs. To control which documents your items can appear in, specify the `documentUrlPatterns` field when you call the `create()` or `update()` methods.

You can create as many context menu items as you need, but if more than one from your extension is visible at once, Google Chrome automatically collapses them into a single parent menu.

## Examples

To try this API, install the contextMenus API example from the chrome-extension-samples repository.

## Types

### `ContextType`

Chrome 44+
The different contexts a menu can appear in. Specifying `'all'` is equivalent to the combination of all other contexts except for `'launcher'`. The `'launcher'` context is only supported by apps and is used to add menu items to the context menu that appears when clicking the app icon in the launcher/taskbar/dock/etc. Different platforms might put limitations on what is actually supported in a launcher context menu.

#### Enum

`"all"`
`"page"`
`"frame"`
`"selection"`
`"link"`
`"editable"`
`"image"`
`"video"`
`"audio"`
`"launcher"`
`"browser_action"`
`"page_action"`
`"action"`

### `CreateProperties`

Chrome 123+
Properties of the new context menu item.

#### Properties

*   `checked`
    `boolean` optional
    The initial state of a checkbox or radio button: `true` for selected, `false` for unselected. Only one radio button can be selected at a time in a given group.
*   `contexts`
    `[ContextType, ...ContextType[]]` optional
    List of contexts this menu item will appear in. Defaults to `['page']`.
*   `documentUrlPatterns`
    `string[]` optional
    Restricts the item to apply only to documents or frames whose URL matches one of the given patterns. For details on pattern formats, see Match Patterns.
*   `enabled`
    `boolean` optional
    Whether this context menu item is enabled or disabled. Defaults to `true`.
*   `id`
    `string` optional
    The unique ID to assign to this item. Mandatory for event pages. Cannot be the same as another ID for this extension.
*   `parentId`
    `string | number` optional
    The ID of a parent menu item; this makes the item a child of a previously added item.
*   `targetUrlPatterns`
    `string[]` optional
    Similar to `documentUrlPatterns`, filters based on the `src` attribute of `img`, `audio`, and `video` tags and the `href` attribute of `a` tags.
*   `title`
    `string` optional
    The text to display in the item; this is required unless `type` is `separator`. When the context is `selection`, use `%s` within the string to show the selected text. For example, if this parameter's value is `"Translate '%s' to Pig Latin"` and the user selects the word `"cool"`, the context menu item for the selection is `"Translate 'cool' to Pig Latin"`.
*   `type`
    `ItemType` optional
    The type of menu item. Defaults to `normal`.
*   `visible`
    `boolean` optional
    Whether the item is visible in the menu.
*   `onclick`
    `void` optional
    A function that is called back when the menu item is clicked. This is not available inside of a service worker; instead, you should register a listener for `contextMenus.onClicked`.
    The `onclick` function looks like:
    ```javascript
    (info: OnClickData, tab: Tab) => {...}
    ```
    *   `info`
        `OnClickData`
        Information about the item clicked and the context where the click happened.
    *   `tab`
        `Tab`
        The details of the tab where the click took place. This parameter is not present for platform apps.

### `ItemType`

Chrome 44+
The type of menu item.

#### Enum

`"normal"`
`"checkbox"`
`"radio"`
`"separator"`

### `OnClickData`

Information sent when a context menu item is clicked.

#### Properties

*   `checked`
    `boolean` optional
    A flag indicating the state of a checkbox or radio item after it is clicked.
*   `editable`
    `boolean`
    A flag indicating whether the element is editable (text input, textarea, etc.).
*   `frameId`
    `number` optional
    Chrome 51+
    The ID of the frame of the element where the context menu was clicked, if it was in a frame.
*   `frameUrl`
    `string` optional
    The URL of the frame of the element where the context menu was clicked, if it was in a frame.
*   `linkUrl`
    `string` optional
    If the element is a link, the URL it points to.
*   `mediaType`
    `string` optional
    One of `'image'`, `'video'`, or `'audio'` if the context menu was activated on one of these types of elements.
*   `menuItemId`
    `string | number`
    The ID of the menu item that was clicked.
*   `pageUrl`
    `string` optional
    The URL of the page where the menu item was clicked. This property is not set if the click occured in a context where there is no current page, such as in a launcher context menu.
*   `parentMenuItemId`
    `string | number` optional
    The parent ID, if any, for the item clicked.
*   `selectionText`
    `string` optional
    The text for the context selection, if any.
*   `srcUrl`
    `string` optional
    Will be present for elements with a `'src'` URL.
*   `wasChecked`
    `boolean` optional
    A flag indicating the state of a checkbox or radio item before it was clicked.

## Properties

### `ACTION_MENU_TOP_LEVEL_LIMIT`

The maximum number of top level extension items that can be added to an extension action context menu. Any items beyond this limit will be ignored.

#### Value

`6`

## Methods

### `create()`

```javascript
chrome.contextMenus.create(
  createProperties: CreateProperties,
  callback?: function,
)
```

Creates a new context menu item. If an error occurs during creation, it may not be detected until the creation callback fires; details will be in `runtime.lastError`.

#### Parameters

*   `createProperties`
    `CreateProperties`
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `number | string`
    The ID of the newly created item.

### `remove()`

Promise

```javascript
chrome.contextMenus.remove(
  menuItemId: string | number,
  callback?: function,
)
```

Removes a context menu item.

#### Parameters

*   `menuItemId`
    `string | number`
    The ID of the context menu item to remove.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 123+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `removeAll()`

Promise

```javascript
chrome.contextMenus.removeAll(
  callback?: function,
)
```

Removes all context menu items added by this extension.

#### Parameters

*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 123+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `update()`

Promise

```javascript
chrome.contextMenus.update(
  id: string | number,
  updateProperties: object,
  callback?: function,
)
```

Updates a previously created context menu item.

#### Parameters

*   `id`
    `string | number`
    The ID of the item to update.
*   `updateProperties`
    `object`
    The properties to update. Accepts the same values as the `contextMenus.create` function.
    *   `checked`
        `boolean` optional
    *   `contexts`
        `[ContextType, ...ContextType[]]` optional
    *   `documentUrlPatterns`
        `string[]` optional
    *   `enabled`
        `boolean` optional
    *   `parentId`
        `string | number` optional
        The ID of the item to be made this item's parent. Note: You cannot set an item to become a child of its own descendant.
    *   `targetUrlPatterns`
        `string[]` optional
    *   `title`
        `string` optional
    *   `type`
        `ItemType` optional
    *   `visible`
        `boolean` optional
        Chrome 62+
        Whether the item is visible in the menu.
    *   `onclick`
        `void` optional
        The `onclick` function looks like:
        ```javascript
        (info: OnClickData, tab: Tab) => {...}
        ```
        *   `info`
            `OnClickData`
            Chrome 44+
        *   `tab`
            `Tab`
            Chrome 44+
            The details of the tab where the click took place. This parameter is not present for platform apps.
*   `callback`
    `function` optional
    The callback parameter looks like:
    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`
    Chrome 123+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onClicked`

```javascript
chrome.contextMenus.onClicked.addListener(
  callback: function,
)
```

Fired when a context menu item is clicked.

#### Parameters

*   `callback`
    `function`
    The callback parameter looks like:
    ```javascript
    (info: OnClickData, tab?: tabs.Tab) => void
    ```
    *   `info`
        `OnClickData`
    *   `tab`
        `tabs.Tab` optional

===

---
title: chrome.cookies
url: https://developer.chrome.com/docs/extensions/reference/api/cookies
---

# chrome.cookies

## Description

Use the `chrome.cookies` API to query and modify cookies, and to be notified when they change.

## Permissions

`cookies`

To use the cookies API, declare the `"cookies"` permission in your manifest along with host permissions for any hosts whose cookies you want to access. For example:

```json
{
  "name": "My extension",
  ...
  "host_permissions": [
    "*://*.google.com/"
  ],
  "permissions": [
    "cookies"
  ],
  ...
}
```

## Partitioning

Partitioned cookies allow a site to mark that certain cookies should be keyed against the origin of the top-level frame. This means that, for example, if site A is embedded using an iframe in site B and site C, the embedded versions of a partitioned cookie from A can have different values on B and C.

By default, all API methods operate on unpartitioned cookies. The `partitionKey` property can be used to override this behavior.

For details on the general impact of partitioning for extensions, see Storage and Cookies.

## Examples

You can find a simple example of using the cookies API in the `examples/api/cookies` directory. For other examples and for help in viewing the source code, see Samples.

## Types

### `Cookie`

Represents information about an HTTP cookie.

#### Properties

*   `domain`

    `string`

    The domain of the cookie (e.g. `"www.google.com"`, `"example.com"`).
*   `expirationDate`

    `number` optional

    The expiration date of the cookie as the number of seconds since the UNIX epoch. Not provided for session cookies.
*   `hostOnly`

    `boolean`

    True if the cookie is a host-only cookie (i.e. a request's host must exactly match the domain of the cookie).
*   `httpOnly`

    `boolean`

    True if the cookie is marked as `HttpOnly` (i.e. the cookie is inaccessible to client-side scripts).
*   `name`

    `string`

    The name of the cookie.
*   `partitionKey`

    `CookiePartitionKey` optional

    Chrome 119+

    The partition key for reading or modifying cookies with the Partitioned attribute.
*   `path`

    `string`

    The path of the cookie.
*   `sameSite`

    `SameSiteStatus`

    Chrome 51+

    The cookie's same-site status (i.e. whether the cookie is sent with cross-site requests).
*   `secure`

    `boolean`

    True if the cookie is marked as Secure (i.e. its scope is limited to secure channels, typically HTTPS).
*   `session`

    `boolean`

    True if the cookie is a session cookie, as opposed to a persistent cookie with an expiration date.
*   `storeId`

    `string`

    The ID of the cookie store containing this cookie, as provided in `getAllCookieStores()`.
*   `value`

    `string`

    The value of the cookie.

### `CookieDetails`

Chrome 88+

Details to identify the cookie.

#### Properties

*   `name`

    `string`

    The name of the cookie to access.
*   `partitionKey`

    `CookiePartitionKey` optional

    Chrome 119+

    The partition key for reading or modifying cookies with the Partitioned attribute.
*   `storeId`

    `string` optional

    The ID of the cookie store in which to look for the cookie. By default, the current execution context's cookie store will be used.
*   `url`

    `string`

    The URL with which the cookie to access is associated. This argument may be a full URL, in which case any data following the URL path (e.g. the query string) is simply ignored. If host permissions for this URL are not specified in the manifest file, the API call will fail.

### `CookiePartitionKey`

Chrome 119+

Represents a partitioned cookie's partition key.

#### Properties

*   `hasCrossSiteAncestor`

    `boolean` optional

    Chrome 130+

    Indicates if the cookie was set in a cross-cross site context. This prevents a top-level site embedded in a cross-site context from accessing cookies set by the top-level site in a same-site context.
*   `topLevelSite`

    `string` optional

    The top-level site the partitioned cookie is available in.

### `CookieStore`

Represents a cookie store in the browser. An incognito mode window, for instance, uses a separate cookie store from a non-incognito window.

#### Properties

*   `id`

    `string`

    The unique identifier for the cookie store.
*   `tabIds`

    `number[]`

    Identifiers of all the browser tabs that share this cookie store.

### `FrameDetails`

Chrome 132+

Details to identify the frame.

#### Properties

*   `documentId`

    `string` optional

    The unique identifier for the document. If the `frameId` and/or `tabId` are provided they will be validated to match the document found by provided document ID.
*   `frameId`

    `number` optional

    The unique identifier for the frame within the tab.
*   `tabId`

    `number` optional

    The unique identifier for the tab containing the frame.

### `OnChangedCause`

Chrome 44+

The underlying reason behind the cookie's change. If a cookie was inserted, or removed via an explicit call to `"chrome.cookies.remove"`, `"cause"` will be `"explicit"`. If a cookie was automatically removed due to expiry, `"cause"` will be `"expired"`. If a cookie was removed due to being overwritten with an already-expired expiration date, `"cause"` will be set to `"expired_overwrite"`. If a cookie was automatically removed due to garbage collection, `"cause"` will be `"evicted"`. If a cookie was automatically removed due to a `"set"` call that overwrote it, `"cause"` will be `"overwrite"`. Plan your response accordingly.

#### Enum

*   `"evicted"`
*   `"expired"`
*   `"explicit"`
*   `"expired_overwrite"`
*   `"overwrite"`

### `SameSiteStatus`

Chrome 51+

A cookie's 'SameSite' state (https://tools.ietf.org/html/draft-west-first-party-cookies). `no_restriction` corresponds to a cookie set with `SameSite=None`, `lax` to `SameSite=Lax`, and `strict` to `SameSite=Strict`. `unspecified` corresponds to a cookie set without the SameSite attribute.

#### Enum

*   `"no_restriction"`
*   `"lax"`
*   `"strict"`
*   `"unspecified"`

## Methods

### `get()`

Promise

```javascript
chrome.cookies.get(
  details: CookieDetails,
  callback?: function,
)
```

Retrieves information about a single cookie. If more than one cookie of the same name exists for the given URL, the one with the longest path will be returned. For cookies with the same path length, the cookie with the earliest creation time will be returned.

#### Parameters

*   `details`

    `CookieDetails`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (cookie?: Cookie) => void
    ```

    *   `cookie`

        `Cookie` optional

        Contains details about the cookie. This parameter is null if no such cookie was found.

#### Returns

*   `Promise<Cookie | undefined>`

    Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAll()`

Promise

```javascript
chrome.cookies.getAll(
  details: object,
  callback?: function,
)
```

Retrieves all cookies from a single cookie store that match the given information. The cookies returned will be sorted, with those with the longest path first. If multiple cookies have the same path length, those with the earliest creation time will be first. This method only retrieves cookies for domains that the extension has host permissions to.

#### Parameters

*   `details`

    `object`

    Information to filter the cookies being retrieved.

    *   `domain`

        `string` optional

        Restricts the retrieved cookies to those whose domains match or are subdomains of this one.
    *   `name`

        `string` optional

        Filters the cookies by name.
    *   `partitionKey`

        `CookiePartitionKey` optional

        Chrome 119+

        The partition key for reading or modifying cookies with the Partitioned attribute.
    *   `path`

        `string` optional

        Restricts the retrieved cookies to those whose path exactly matches this string.
    *   `secure`

        `boolean` optional

        Filters the cookies by their Secure property.
    *   `session`

        `boolean` optional

        Filters out session vs. persistent cookies.
    *   `storeId`

        `string` optional

        The cookie store to retrieve cookies from. If omitted, the current execution context's cookie store will be used.
    *   `url`

        `string` optional

        Restricts the retrieved cookies to those that would match the given URL.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (cookies: Cookie[]) => void
    ```

    *   `cookies`

        `Cookie[]`

        All the existing, unexpired cookies that match the given cookie info.

#### Returns

*   `Promise<Cookie[]>`

    Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAllCookieStores()`

Promise

```javascript
chrome.cookies.getAllCookieStores(
  callback?: function,
)
```

Lists all existing cookie stores.

#### Parameters

*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (cookieStores: CookieStore[]) => void
    ```

    *   `cookieStores`

        `CookieStore[]`

        All the existing cookie stores.

#### Returns

*   `Promise<CookieStore[]>`

    Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getPartitionKey()`

Promise Chrome 132+

```javascript
chrome.cookies.getPartitionKey(
  details: FrameDetails,
  callback?: function,
)
```

The partition key for the frame indicated.

#### Parameters

*   `details`

    `FrameDetails`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        `object`

        Contains details about the partition key that's been retrieved.

        *   `partitionKey`

            `CookiePartitionKey`

            The partition key for reading or modifying cookies with the Partitioned attribute.

#### Returns

*   `Promise<object>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `remove()`

Promise

```javascript
chrome.cookies.remove(
  details: CookieDetails,
  callback?: function,
)
```

Deletes a cookie by name.

#### Parameters

*   `details`

    `CookieDetails`
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (details?: object) => void
    ```

    *   `details`

        `object` optional

        Contains details about the cookie that's been removed. If removal failed for any reason, this will be `"null"`, and `runtime.lastError` will be set.

        *   `name`

            `string`

            The name of the cookie that's been removed.
        *   `partitionKey`

            `CookiePartitionKey` optional

            Chrome 119+

            The partition key for reading or modifying cookies with the Partitioned attribute.
        *   `storeId`

            `string`

            The ID of the cookie store from which the cookie was removed.
        *   `url`

            `string`

            The URL associated with the cookie that's been removed.

#### Returns

*   `Promise<object | undefined>`

    Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `set()`

Promise

```javascript
chrome.cookies.set(
  details: object,
  callback?: function,
)
```

Sets a cookie with the given cookie data; may overwrite equivalent cookies if they exist.

#### Parameters

*   `details`

    `object`

    Details about the cookie being set.

    *   `domain`

        `string` optional

        The domain of the cookie. If omitted, the cookie becomes a host-only cookie.
    *   `expirationDate`

        `number` optional

        The expiration date of the cookie as the number of seconds since the UNIX epoch. If omitted, the cookie becomes a session cookie.
    *   `httpOnly`

        `boolean` optional

        Whether the cookie should be marked as `HttpOnly`. Defaults to `false`.
    *   `name`

        `string` optional

        The name of the cookie. Empty by default if omitted.
    *   `partitionKey`

        `CookiePartitionKey` optional

        Chrome 119+

        The partition key for reading or modifying cookies with the Partitioned attribute.
    *   `path`

        `string` optional

        The path of the cookie. Defaults to the path portion of the `url` parameter.
    *   `sameSite`

        `SameSiteStatus` optional

        Chrome 51+

        The cookie's same-site status. Defaults to `"unspecified"`, i.e., if omitted, the cookie is set without specifying a `SameSite` attribute.
    *   `secure`

        `boolean` optional

        Whether the cookie should be marked as Secure. Defaults to `false`.
    *   `storeId`

        `string` optional

        The ID of the cookie store in which to set the cookie. By default, the cookie is set in the current execution context's cookie store.
    *   `url`

        `string`

        The request-URI to associate with the setting of the cookie. This value can affect the default domain and path values of the created cookie. If host permissions for this URL are not specified in the manifest file, the API call will fail.
    *   `value`

        `string` optional

        The value of the cookie. Empty by default if omitted.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (cookie?: Cookie) => void
    ```

    *   `cookie`

        `Cookie` optional

        Contains details about the cookie that's been set. If setting failed for any reason, this will be `"null"`, and `runtime.lastError` will be set.

#### Returns

*   `Promise<Cookie | undefined>`

    Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onChanged`

```javascript
chrome.cookies.onChanged.addListener(
  callback: function,
)
```

Fired when a cookie is set or removed. As a special case, note that updating a cookie's properties is implemented as a two step process: the cookie to be updated is first removed entirely, generating a notification with `"cause"` of `"overwrite"`. Afterwards, a new cookie is written with the updated values, generating a second notification with `"cause"` `"explicit"`.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (changeInfo: object) => void
    ```

    *   `changeInfo`

        `object`

        *   `cause`

            `OnChangedCause`

            The underlying reason behind the cookie's change.
        *   `cookie`

            `Cookie`

            Information about the cookie that was set or removed.
        *   `removed`

            `boolean`

            True if a cookie was removed.

===

---
title: chrome.debugger
url: https://developer.chrome.com/docs/extensions/reference/api/debugger
---

# chrome.debugger

## Description

The `chrome.debugger` API serves as an alternate transport for Chrome's remote debugging protocol. Use `chrome.debugger` to attach to one or more tabs to instrument network interaction, debug JavaScript, mutate the DOM and CSS, and more. Use the `Debuggee` property `tabId` to target tabs with `sendCommand` and route events by `tabId` from `onEvent` callbacks.

## Permissions

`debugger`

You must declare the `"debugger"` permission in your extension's manifest to use this API.

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "debugger"
  ],
  ...
}
```

## Concepts and usage

Once attached, the `chrome.debugger` API lets you send Chrome DevTools Protocol (CDP) commands to a given target. Explaining the CDP in depth is out of scope for this documentation鈥攖o learn more about CDP check out the official CDP documentation.

### Targets

Targets represent something which is being debugged鈥攖his could include a tab, an iframe or a worker. Each target is identified by a UUID and has an associated type (such as `iframe`, `shared_worker`, and more).

Within a target, there may be multiple execution contexts鈥攆or example same process iframes don't get a unique target but are instead represented as different contexts that can be accessed from a single target.

### Restricted domains

For security reasons, the `chrome.debugger` API does not provide access to all Chrome DevTools Protocol Domains. The available domains are: `Accessibility`, `Audits`, `CacheStorage`, `Console`, `CSS`, `Database`, `Debugger`, `DOM`, `DOMDebugger`, `DOMSnapshot`, `Emulation`, `Fetch`, `IO`, `Input`, `Inspector`, `Log`, `Network`, `Overlay`, `Page`, `Performance`, `Profiler`, `Runtime`, `Storage`, `Target`, `Tracing`, `WebAudio`, and `WebAuthn`.

### Work with frames

There is not a one to one mapping of frames to targets. Within a single tab, multiple same process frames may share the same target but use a different execution context. On the other hand, a new target may be created for an out-of-process iframe.

To attach to all frames, you need to handle each type of frame separately:

*   Listen for the `Runtime.executionContextCreated` event to identify new execution contexts associated with same process frames.
*   Follow the steps to attach to related targets to identify out-of-process frames.

### Attach to related targets

After connecting to a target, you may want to connect to further related targets including out-of-process child frames or associated workers.

Starting in Chrome 125, the `chrome.debugger` API supports flat sessions. This lets you add additional targets as children to your main debugger session and message them without needing another call to `chrome.debugger.attach`. Instead, you can add a `sessionId` property when calling `chrome.debugger.sendCommand` to identify the child target you would like to send a command to.

To automatically attach to out of process child frames, first add a listener for the `Target.attachedToTarget` event:

```javascript
chrome.debugger.onEvent.addListener((source, method, params) => {
  if (method === "Target.attachedToTarget") {
    // `source` identifies the parent session, but we need to construct a new
    // identifier for the child session
    const session = {
      ...source,
      sessionId: params.sessionId
    };
    // Call any needed CDP commands for the child session
    await chrome.debugger.sendCommand(session, "Runtime.enable");
  }
});
```

Then, enable auto attach by sending the `Target.setAutoAttach` command with the `flatten` option set to `true`:

```javascript
await chrome.debugger.sendCommand({ tabId }, "Target.setAutoAttach", {
  autoAttach: true,
  waitForDebuggerOnStart: false,
  flatten: true,
  filter: [{ type: "iframe", exclude: false }]
});
```

Auto-attach only attaches to frames the target is aware of, which is limited to frames which are immediate children of a frame associated with it. For example, with the frame hierarchy A -> B -> C (where all are cross-origin), calling `Target.setAutoAttach` for the target associated with A would result in the session also being attached to B. However, this is not recursive, so `Target.setAutoAttach` also needs to be called for B to attach the session to C.

## Examples

To try this API, install the debugger API example from the `chrome-extension-samples` repository.

## Types

### `Debuggee`

Debuggee identifier. Either `tabId`, `extensionId` or `targetId` must be specified

#### Properties

*   `extensionId`

    `string` optional

    The id of the extension which you intend to debug. Attaching to an extension background page is only possible when the `--silent-debugger-extension-api` command-line switch is used.
*   `tabId`

    `number` optional

    The id of the tab which you intend to debug.
*   `targetId`

    `string` optional

    The opaque id of the debug target.

### `DebuggerSession`

Chrome 125+

Debugger session identifier. One of `tabId`, `extensionId` or `targetId` must be specified. Additionally, an optional `sessionId` can be provided. If `sessionId` is specified for arguments sent from `onEvent`, it means the event is coming from a child protocol session within the root debuggee session. If `sessionId` is specified when passed to `sendCommand`, it targets a child protocol session within the root debuggee session.

#### Properties

*   `extensionId`

    `string` optional

    The id of the extension which you intend to debug. Attaching to an extension background page is only possible when the `--silent-debugger-extension-api` command-line switch is used.
*   `sessionId`

    `string` optional

    The opaque id of the Chrome DevTools Protocol session. Identifies a child session within the root session identified by `tabId`, `extensionId` or `targetId`.
*   `tabId`

    `number` optional

    The id of the tab which you intend to debug.
*   `targetId`

    `string` optional

    The opaque id of the debug target.

### `DetachReason`

Chrome 44+

Connection termination reason.

#### Enum

*   `"target_closed"`
*   `"canceled_by_user"`

### `TargetInfo`

Debug target information

#### Properties

*   `attached`

    `boolean`

    True if debugger is already attached.
*   `extensionId`

    `string` optional

    The extension id, defined if `type` = `'background_page'`.
*   `faviconUrl`

    `string` optional

    Target favicon URL.
*   `id`

    `string`

    Target id.
*   `tabId`

    `number` optional

    The tab id, defined if `type` == `'page'`.
*   `title`

    `string`

    Target page title.
*   `type`

    `TargetInfoType`

    Target type.
*   `url`

    `string`

    Target URL.

### `TargetInfoType`

Chrome 44+

Target type.

#### Enum

*   `"page"`
*   `"background_page"`
*   `"worker"`
*   `"other"`

## Methods

### `attach()`

Promise

```javascript
chrome.debugger.attach(
  target: Debuggee,
  requiredVersion: string,
  callback?: function,
)
```

Attaches debugger to the given target.

#### Parameters

*   `target`

    `Debuggee`

    Debugging target to which you want to attach.
*   `requiredVersion`

    `string`

    Required debugging protocol version (`"0.1"`). One can only attach to the debuggee with matching major version and greater or equal minor version. List of the protocol versions can be obtained here.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `detach()`

Promise

```javascript
chrome.debugger.detach(
  target: Debuggee,
  callback?: function,
)
```

Detaches debugger from the given target.

#### Parameters

*   `target`

    `Debuggee`

    Debugging target from which you want to detach.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getTargets()`

Promise

```javascript
chrome.debugger.getTargets(
  callback?: function,
)
```

Returns the list of available debug targets.

#### Parameters

*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result: TargetInfo[]) => void
    ```

    *   `result`

        `TargetInfo[]`

        Array of `TargetInfo` objects corresponding to the available debug targets.

#### Returns

*   `Promise<TargetInfo[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `sendCommand()`

Promise

```javascript
chrome.debugger.sendCommand(
  target: DebuggerSession,
  method: string,
  commandParams?: object,
  callback?: function,
)
```

Sends given command to the debugging target.

#### Parameters

*   `target`

    `DebuggerSession`

    Debugging target to which you want to send the command.
*   `method`

    `string`

    Method name. Should be one of the methods defined by the remote debugging protocol.
*   `commandParams`

    `object` optional

    JSON object with request parameters. This object must conform to the remote debugging params scheme for given method.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result?: object) => void
    ```

    *   `result`

        `object` optional

        JSON object with the response. Structure of the response varies depending on the method name and is defined by the `'returns'` attribute of the command description in the remote debugging protocol.

#### Returns

*   `Promise<object | undefined>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onDetach`

```javascript
chrome.debugger.onDetach.addListener(
  callback: function,
)
```

Fired when browser terminates debugging session for the tab. This happens when either the tab is being closed or Chrome DevTools is being invoked for the attached tab.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (source: Debuggee, reason: DetachReason) => void
    ```

    *   `source`

        `Debuggee`
    *   `reason`

        `DetachReason`

### `onEvent`

```javascript
chrome.debugger.onEvent.addListener(
  callback: function,
)
```

Fired whenever debugging target issues instrumentation event.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (source: DebuggerSession, method: string, params?: object) => void
    ```

    *   `source`

        `DebuggerSession`
    *   `method`

        `string`
    *   `params`

        `object` optional

===

---
title: chrome.declarativeContent
url: https://developer.chrome.com/docs/extensions/reference/api/declarativeContent
---

## Description

Use the `chrome.declarativeContent` API to take actions depending on the content of a page, without requiring permission to read the page's content.

## Permissions

`declarativeContent`

## Concepts and usage

Key term: An extension's action controls the extension's toolbar icon.

The Declarative Content API lets you enable your extension's action depending on the URL of a web page, or if a CSS selector matches an element on the page, without needing to add host permissions or inject a content script.

Use the `activeTab` permission to interact with a page after the user clicks on the extension's action.

### Rules

Rules consists of conditions and actions. If any of the conditions is fulfilled, all actions are executed. The actions are `setIcon()` and `showAction()`.

The `PageStateMatcher` matches web pages if and only if all listed criteria are met. It can match a page url, a css compound selector or the bookmarked state of a page. The following rule enables the extension's action on Google pages when a password field is present:

```javascript
let rule1 = {
  conditions: [
    new chrome.declarativeContent.PageStateMatcher({
      pageUrl: { hostSuffix: '.google.com', schemes: ['https'] },
      css: ["input[type='password']"]
    })
  ],
  actions: [ new chrome.declarativeContent.ShowAction() ]
};
```

Success: All conditions and actions are created using a constructor as shown in the previous example.

To also enable the extension's action for Google sites with a video, you can add a second condition, as each condition is sufficient to trigger all specified actions:

```javascript
let rule2 = {
  conditions: [
    new chrome.declarativeContent.PageStateMatcher({
      pageUrl: { hostSuffix: '.google.com', schemes: ['https'] },
      css: ["input[type='password']"]
    }),
    new chrome.declarativeContent.PageStateMatcher({
      css: ["video"]
    })
  ],
  actions: [ new chrome.declarativeContent.ShowAction() ]
};
```

The `onPageChanged` event tests whether any rule has at least one fulfilled condition and executes the actions. Rules persist across browsing sessions; therefore, during extension installation time you should first use `removeRules` to clear previously installed rules and then use `addRules` to register new ones.

```javascript
chrome.runtime.onInstalled.addListener(function(details) {
  chrome.declarativeContent.onPageChanged.removeRules(undefined, function() {
    chrome.declarativeContent.onPageChanged.addRules([rule2]);
  });
});
```

Note: You should always register or unregister rules in bulk because each of these operations recreates internal data structures. This re-creation is computationally expensive but facilitates a faster matching algorithm.

With the `activeTab` permission, your extension won't display any permission warnings and when the user clicks the extension action, it will only run on relevant pages.

### Page URL matching

The `PageStateMatcher.pageUrl` matches when the URL criteria are fulfilled. The most common criteria are a concatenation of either `host`, `path`, or `URL`, followed by `Contains`, `Equals`, `Prefix`, or `Suffix`. The following table contains a few examples:

| Criteria | Matches |
| --- | --- |
| `{ hostSuffix: 'google.com' }` | All Google URLs |
| `{ pathPrefix: '/docs/extensions' }` | Extension docs URLs |
| `{ urlContains: 'developer.chrome.com' }` | All chrome developers docs URLs |

All criteria are case sensitive. For a complete list of criteria, see `UrlFilter`.

### CSS Matching

`PageStateMatcher.css` conditions must be compound selectors, meaning that you can't include combinators like whitespace or `>` in your selectors. This helps Chrome match the selectors more efficiently.

| Compound Selectors (OK) | Complex Selectors (Not OK) |
| --- | --- |
| `a` | `div p` |
| `iframe.special[src^='http']` | `p>span.highlight` |
| `ns|\*` | `p + ol` |
| `#abcd:checked` | `p::first-line` |

CSS conditions only match displayed elements: if an element that matches your selector is `display:none` or one of its parent elements is `display:none`, it doesn't cause the condition to match. Elements styled with `visibility:hidden`, positioned off-screen, or hidden by other elements can still make your condition match.

### Bookmarked state matching

The `PageStateMatcher.isBookmarked` condition allows matching of the bookmarked state of the current URL in the user's profile. To make use of this condition the `"bookmarks"` permission must be declared in the extension manifest.

## Types

### ImageDataType

See `https://developer.mozilla.org/en-US/docs/Web/API/ImageData`.

#### Type

`ImageData`

### PageStateMatcher

Matches the state of a web page based on various criteria.

#### Properties

*   `constructor`

    `void`

    The constructor function looks like:

    ```javascript
    (arg: PageStateMatcher) => {...}
    ```

    *   `arg`

        `PageStateMatcher`

    *   returns

        `PageStateMatcher`
*   `css`

    `string[]` optional

    Matches if all of the CSS selectors in the array match displayed elements in a frame with the same origin as the page's main frame. All selectors in this array must be compound selectors to speed up matching. Note: Listing hundreds of CSS selectors or listing CSS selectors that match hundreds of times per page can slow down web sites.
*   `isBookmarked`

    `boolean` optional

    Chrome 45+

    Matches if the bookmarked state of the page is equal to the specified value. Requres the `bookmarks` permission.
*   `pageUrl`

    `UrlFilter` optional

    Matches if the conditions of the `UrlFilter` are fulfilled for the top-level URL of the page.

### RequestContentScript

Declarative event action that injects a content script.

WARNING: This action is still experimental and is not supported on stable builds of Chrome.

#### Properties

*   `constructor`

    `void`

    The constructor function looks like:

    ```javascript
    (arg: RequestContentScript) => {...}
    ```

    *   `arg`

        `RequestContentScript`

    *   returns

        `RequestContentScript`
*   `allFrames`

    `boolean` optional

    Whether the content script runs in all frames of the matching page, or in only the top frame. Default is `false`.
*   `css`

    `string[]` optional

    Names of CSS files to be injected as a part of the content script.
*   `js`

    `string[]` optional

    Names of JavaScript files to be injected as a part of the content script.
*   `matchAboutBlank`

    `boolean` optional

    Whether to insert the content script on `about:blank` and `about:srcdoc`. Default is `false`.

### SetIcon

Declarative event action that sets the n-dip square icon for the extension's page action or browser action while the corresponding conditions are met. This action can be used without host permissions, but the extension must have a page or browser action.

Exactly one of `imageData` or `path` must be specified. Both are dictionaries mapping a number of pixels to an image representation. The image representation in `imageData` is an `ImageData` object; for example, from a canvas element, while the image representation in `path` is the path to an image file relative to the extension's manifest. If scale screen pixels fit into a device-independent pixel, the `scale * n` icon is used. If that scale is missing, another image is resized to the required size.

#### Properties

*   `constructor`

    `void`

    The constructor function looks like:

    ```javascript
    (arg: SetIcon) => {...}
    ```

    *   `arg`

        `SetIcon`

    *   returns

        `SetIcon`
*   `imageData`

    `ImageData` | `object` optional

    Either an `ImageData` object or a dictionary `{size -> ImageData}` representing an icon to be set. If the icon is specified as a dictionary, the image used is chosen depending on the screen's pixel density. If the number of image pixels that fit into one screen space unit equals `scale`, then an image with size `scale * n` is selected, where `n` is the size of the icon in the UI. At least one image must be specified. Note that `details.imageData = foo` is equivalent to `details.imageData = {'16': foo}`.

### ShowAction

Chrome 97+

A declarative event action that sets the extension's toolbar action to an enabled state while the corresponding conditions are met. This action can be used without host permissions. If the extension has the `activeTab` permission, clicking the page action grants access to the active tab.

On pages where the conditions are not met the extension's toolbar action will be grey-scale, and clicking it will open the context menu, instead of triggering the action.

#### Properties

*   `constructor`

    `void`

    The constructor function looks like:

    ```javascript
    (arg: ShowAction) => {...}
    ```

    *   `arg`

        `ShowAction`

    *   returns

        `ShowAction`

### ShowPageAction

Deprecated since Chrome 97

Please use `declarativeContent.ShowAction`.

A declarative event action that sets the extension's page action to an enabled state while the corresponding conditions are met. This action can be used without host permissions, but the extension must have a page action. If the extension has the `activeTab` permission, clicking the page action grants access to the active tab.

On pages where the conditions are not met the extension's toolbar action will be grey-scale, and clicking it will open the context menu, instead of triggering the action.

#### Properties

*   `constructor`

    `void`

    The constructor function looks like:

    ```javascript
    (arg: ShowPageAction) => {...}
    ```

    *   `arg`

        `ShowPageAction`

    *   returns

        `ShowPageAction`

## Events

### onPageChanged

Provides the Declarative Event API consisting of `addRules`, `removeRules`, and `getRules`.

#### Conditions

`PageStateMatcher`

#### Actions

`RequestContentScript`

`SetIcon`

`ShowPageAction`

`ShowAction`

===

---
title: chrome.declarativeNetRequest
url: https://developer.chrome.com/docs/extensions/reference/api/declarativeNetRequest
---

## Description

The `chrome.declarativeNetRequest` API is used to block or modify network requests by specifying declarative rules. This lets extensions modify network requests without intercepting them and viewing their content, thus providing more privacy.

## Permissions

`declarativeNetRequest` `declarativeNetRequestWithHostAccess`

The `"declarativeNetRequest"` and `"declarativeNetRequestWithHostAccess"` permissions provide the same capabilities. The differences between them is when permissions are requested or granted.

`"declarativeNetRequest"`
:   Triggers a permission warning at install time but provides implicit access to `allow`, `allowAllRequests` and `block` rules. Use this when possible to avoid needing to request full access to hosts.

`"declarativeNetRequestFeedback"`
:   Enables debugging features for unpacked extensions, specifically `getMatchedRules()` and `onRuleMatchedDebug`.

`"declarativeNetRequestWithHostAccess"`
:   A permission warning is not shown at install time, but you must request host permissions before you can perform any action on a host. This is appropriate when you want to use declarative net request rules in an extension which already has host permissions without generating additional warnings.

## Availability

Chrome 84+

## Manifest

In addition to the permissions described previously, certain types of rulesets, static rulesets specifically, require declaring the `"declarative_net_request"` manifest key, which should be a dictionary with a single key called `"rule_resources"`. This key is an array containing dictionaries of type `Ruleset`, as shown in the following. (Note that the name '`Ruleset`' does not appear in the manifest's JSON since it is merely an array.) Static rulesets are explained later in this document.

```json
{
  "name": "My extension",
  ...
  "declarative_net_request" : {
    "rule_resources" : [
      {
        "id": "ruleset_1",
        "enabled": true,
        "path": "rules_1.json"
      },
      {
        "id": "ruleset_2",
        "enabled": false,
        "path": "rules_2.json"
      }
    ]
  },
  "permissions": [
    "declarativeNetRequest",
    "declarativeNetRequestFeedback"
  ],
  "host_permissions": [
    "http://www.blogger.com/*",
    "http://*.google.com/*"
  ],
  ...
}
```

## Rules and rulesets

To use this API, specify one or more rulesets. A ruleset contains an array of rules. A single rule does one of the following:

*   Block a network request.
*   Upgrade the schema (http to https).
*   Prevent a request from getting blocked by negating any matching blocked rules.
*   Redirect a network request.
*   Modify request or response headers.

There are three types of rulesets, managed in slightly different ways.

`Dynamic`
:   Persist across browser sessions and extension upgrades and are managed using JavaScript while an extension is in use.

`Session`
:   Cleared when the browser shuts down and when a new version of the extension is installed. Session rules are managed using JavaScript while an extension is in use.

`Static`
:   Packaged, installed, and updated when an extension is installed or upgraded. Static rules are stored in JSON-formatted rule files and listed in the manifest file.

### Dynamic and session-scoped rulesets

Dynamic and session rulesets are managed using JavaScript while an extension is in use.

*   Dynamic rules persist across browser sessions and extension upgrades.
*   Session rules are cleared when the browser shuts down and when a new version of the extension is installed.

There is only one each of these ruleset types. An extension can add or remove rules to them dynamically by calling `updateDynamicRules()` and `updateSessionRules()`, provided the rule limits aren't exceeded. For information on rule limits, see Rule limits. You can see an example of this under code examples.

### Static rulesets

Unlike dynamic and session rules, static rules are packaged, installed, and updated when an extension is installed or upgraded. They're stored in rule files in JSON format, which are indicated to the extension using the `"declarative_net_request"` and `"rule_resources"` keys as described above, as well as one or more `Ruleset` dictionaries. A `Ruleset` dictionary contains a path to the rule file, an ID for the ruleset contained in the file, and whether the ruleset is enabled or disabled. The last two are important when you enable or disable a ruleset programmatically.

```json
{
  ...
  "declarative_net_request" : {
    "rule_resources" : [
      {
        "id": "ruleset_1",
        "enabled": true,
        "path": "rules_1.json"
      },
      ...
    ]
  }
  ...
}
```

To test rule files, load your extension unpacked. Errors and warnings about invalid static rules are only displayed for unpacked extensions. Invalid static rules in packed extensions are ignored.

## Expedited review

Changes to static rulesets may be eligible for expedited review. See expedited review for eligible changes.

## Enable and disable static rules and rulesets

Both individual static rules and complete static rulesets may be enabled or disabled at runtime.

The set of enabled static rules and rulesets is persisted across browser sessions. Neither are persisted across extension updates, meaning that only rules you chose to leave in your rule files are available after an update.

For performance reasons there are also limits to the number of rules and rulesets that may be enabled at one time. Call `getAvailableStaticRuleCount()` to check the number of additional rules that may be enabled. For information on rule limits, see Rule limits.

To enable or disable static rules, call `updateStaticRules()`. This method takes an `UpdateStaticRulesOptions` object, which contains arrays of IDs of rules to enable or disable. The IDs are defined using the `"id"` key of the `Ruleset` dictionary. There is a maximum limit of 5000 disabled static rules.

To enable or disable static rulesets, call `updateEnabledRulesets()`. This method takes an `UpdateRulesetOptions` object, which contains arrays of IDs of rulesets to enable or disable. The IDs are defined using the `"id"` key of the `Ruleset` dictionary.

## Build rules

Regardless of type, a rule starts with four fields as shown in the following. While the `"id"` and `"priority"` keys take a number, the `"action"` and `"condition"` keys may provide several blocking and redirecting conditions. The following rule blocks all script requests originating from `"foo.com"` to any URL with `"abc"` as a substring.

```json
{
  "id" : 1,
  "priority": 1,
  "action" : { "type" : "block" },
  "condition" : {
    "urlFilter" : "abc",
    "initiatorDomains" : ["foo.com"],
    "resourceTypes" : ["script"]
  }
}
```

## URL matching

Declarative Net Request provides the ability to match URLs with either a pattern matching syntax or regular expressions.

### URL filter syntax

A rule's `"condition"` key allows a `"urlFilter"` key for acting on URLs under a specified domain. You create patterns using pattern matching tokens. Here are a few examples.

| `urlFilter`         | Matches                                         | Does not match        |
| ------------------- | ----------------------------------------------- | --------------------- |
| `"abc"`             | `https://abcd.com` `https://example.com/abcd`   | `https://ab.com`      |
| `"abc*d"`           | `https://abcd.com` `https://example.com/abcxyzd`| `https://abc.com`     |
| `"||a.example.com"` | `https://a.example.com/` `https://b.a.example.com/xyz` `https://a.example.company` | `https://example.com/`|
| `"|https*"`         | `https://example.com`                           | `http://example.com/` `http://https.com` |
| `"example*^123|"`   | `https://example.com/123` `http://abc.com/example?123` | `https://example.com/1234` `https://abc.com/example0123` |

### Regular expressions

Conditions can also use regular expressions. See the `"regexFilter"` key. To learn about the limits that apply to these conditions, see Rules that use regular expressions.

### Write good URL conditions

Take care when writing rules to always match an entire domain. Otherwise, your rule may match in situations that are unexpected. For example, when using the pattern matching syntax:

*   `google.com` incorrectly matches `https://example.com/?param=google.com`
*   `||google.com` incorrectly matches `https://google.company`
*   `https://www.google.com` incorrectly matches `https://example.com/?param=https://www.google.com`

Consider using:

*   `||google.com/`, which matches all paths and all subdomains.
*   `|https://www.google.com/` which matches all paths and no subdomains.

Similarly, use the `^` and `/` characters to anchor a regular expression. For example, `^https:\/\/www\.google\.com\/` matches any path on `https://www.google.com`.

## Rule evaluation

DNR rules are applied by the browser across various stages of the network request lifecycle.

### Before the request

Before a request is made, an extension can block or redirect (including upgrading the scheme from HTTP to HTTPS) it with a matching rule.

For each extension, the browser determines a list of matching rules. Rules with a `modifyHeaders` action are not included here as they will be handled later. Additionally, rules with a `responseHeaders` condition will be considered later (when response headers are available) and are not included.

Then, for each extension, Chrome picks at most one candidate per request. Chrome finds a matching rule, by ordering all matching rules by priority. Rules with the same priority are ordered by action (`allow` or `allowAllRequests` > `block` > `upgradeScheme` > `redirect`).

If the candidate is an `allow` or `allowAllRequests` rule, or the frame the request is being made in previously matched an `allowAllRequests` rule of higher or equal priority from this extension, the request is "allowed" and the extension won't have any effect on the request.

If more than one extension wants to block or redirect this request, a single action to take is chosen. Chrome does this by sorting the rules in the order `block` > `redirect` or `upgradeScheme` > `allow` or `allowAllRequests`. If two rules are of the same type, Chrome chooses the rule from the most recently installed extension.

Caution: Browser vendors have agreed not to standardize the order in which rules with the same action and priority run. This can change between runs or browser versions, even when spread between multiple types of ruleset (such as a static rule and a session rule). When ordering is important, you should always explicitly specify a priority.

### Before request headers are sent

Before Chrome sends request headers to the server, the headers are updated based on matching `modifyHeaders` rules.

Within a single extension, Chrome builds the list of modifications to perform by finding all matching `modifyHeaders` rules. Similar to before, only rules which have a higher priority than any matching `allow` or `allowAllRequests` rules are included.

These rules are applied by Chrome in an order such that rules from a more recently installed extension are always evaluated before rules from an older extension. Additionally, rules of a higher priority from one extension are always applied before rules of a lower priority from the same extension. Notably, even across extensions:

*   If a rule appends to a header, then lower priority rules can only append to that header. `Set` and `remove` operations are not allowed.
*   If a rule sets a header, then only lower priority rules from the same extension can append to that header. No other modifications are allowed.
*   If a rule removes a header, then lower priority rules cannot further modify the header.

### Once a response is received

Once the response headers have been received, Chrome evaluates rules with a `responseHeaders` condition.

After sorting these rules by action and priority and excluding any rules made redundant by a matching `allow` or `allowAllRequests` rule (this happens identically to the steps in "Before the request"), Chrome may block or redirect the request on behalf of an extension.

Note that if a request made it to this stage, the request has already been sent to the server and the server has received data like the request body. A `block` or `redirect` rule with a response headers condition will still run鈥揵ut cannot actually block or redirect the request.

In the case of a `block` rule, this is handled by the page which made the request receiving a blocked response and Chrome terminating the request early. In the case of a `redirect` rule, Chrome makes a new request to the redirected URL. Make sure to consider if these behaviors meet the privacy expectations for your extension.

If the request is not blocked or redirected, Chrome applies any `modifyHeaders` rules. Applying modifications to response headers works in the same way as described in "Before request headers are sent". Applying modifications to request headers does nothing, since the request has already been made.

## Safe rules

Safe rules are defined as rules with an action of `block`, `allow`, `allowAllRequests` or `upgradeScheme`. These rules are subject to an increased dynamic rules quota.

## Rule limits

There is a performance overhead to loading and evaluating rules in the browser, so some limits apply when using the API. Limits depend on the type of rule you're using.

### Static rules

Static rules are those specified in rule files declared in the manifest file. An extension can specify up to 100 static rulesets as part of the `"rule_resources"` manifest key, but only 50 of these rulesets can be enabled at a time. The latter is called the `MAX_NUMBER_OF_ENABLED_STATIC_RULESETS`. Collectively, those rulesets are guaranteed at least 30,000 rules. This is called the `GUARANTEED_MINIMUM_STATIC_RULES`.

Note: Prior to Chrome 120, extensions were limited to a total of 50 static rulesets, and only 10 of these could be enabled at the same time. Use the `minimum_chrome_version` manifest field to limit which Chrome versions can install your extension.

The number of rules available after that depends on how many rules are enabled by all the extensions installed on a user's browser. You can find this number at runtime by calling `getAvailableStaticRuleCount()`. You can see an example of this under code examples.

Note: Starting with Chrome 128, if a user disables an extension through `chrome://extensions`, the extension's static rules will no longer count towards the global static rule limit. This potentially frees up static rule quota for other extensions, but also means that when the extension gets re-enabled, it might have fewer static rules available than before.

### Session rules

An extension can have up to 5000 session rules. This is exposed as the `MAX_NUMBER_OF_SESSION_RULES`.

Before Chrome 120, there was a limit of 5000 combined dynamic and session rules.

### Dynamic rules

An extension can have at least 5000 dynamic rules. This is exposed as the `MAX_NUMBER_OF_UNSAFE_DYNAMIC_RULES`.

Starting in Chrome 121, there is a larger limit of 30,000 rules available for safe dynamic rules, exposed as the `MAX_NUMBER_OF_DYNAMIC_RULES`. Any unsafe rules added within the limit of 5000 will also count towards this limit.

Before Chrome 120, there was a 5000 combined dynamic and session rules limit.

### Rules that use regular expressions

All types of rules can use regular expressions; however, the total number of regular expression rules of each type cannot exceed 1000. This is called the `MAX_NUMBER_OF_REGEX_RULES`.

Additionally, each rule must be less than 2KB once compiled. This roughly correlates with the complexity of the rule. If you try to load a rule that exceeds this limit, you will see a warning like the following and the rule will be ignored.

```
rules_1.json: Rule with id 1 specified a more complex regex than allowed as part of the "regexFilter" key.
```

## Interactions with service workers

A `declarativeNetRequest` only applies to requests that reach the network stack. This includes responses from the HTTP cache, but may not include responses that go through a service worker's `onfetch` handler. `declarativeNetRequest` won't affect responses generated by the service worker or retrieved from `CacheStorage`, but it will affect calls to `fetch()` made in a service worker.

## Web accessible resources

A `declarativeNetRequest` rule cannot redirect from a public resource request to a resource that is not web accessible. Doing so triggers an error. This is true even if the specified web accessible resource is owned by the redirecting extension. To declare resources for `declarativeNetRequest`, use the manifest's `"web_accessible_resources"` array.

## Header modification

The `append` operation is only supported for the following headers: `accept`, `accept-encoding`, `accept-language`, `access-control-request-headers`, `cache-control`, `connection`, `content-language`, `cookie`, `forwarded`, `if-match`, `if-none-match`, `keep-alive`, `range`, `te`, `trailer`, `transfer-encoding`, `upgrade`, `user-agent`, `via`, `want-digest`, `x-forwarded-for`.

## Examples

### Code examples

#### Update dynamic rules

The following example shows how to call `updateDynamicRules()`. The procedure for `updateSessionRules()` is the same.

```javascript
// Get arrays containing new and old rules
const newRules = await getNewRules();
const oldRules = await chrome.declarativeNetRequest.getDynamicRules();
const oldRuleIds = oldRules.map(rule => rule.id);

// Use the arrays to update the dynamic rules
await chrome.declarativeNetRequest.updateDynamicRules({
  removeRuleIds: oldRuleIds,
  addRules: newRules
});
```

#### Update static rulesets

The following example shows how to enable and disable rulesets while considering the number of available and the maximum number of enabled static rulesets. You would do this when the number of static rules you need exceeds the number allowed. For this to work, some of your rulesets should be installed with some of your rulesets disabled (setting `"Enabled"` to `false` within the manifest file).

```javascript
async function updateStaticRules(enableRulesetIds, disableCandidateIds) {
  // Create the options structure for the call to updateEnabledRulesets()
  let options = {
    enableRulesetIds: enableRulesetIds
  }

  // Get the number of enabled static rules
  const enabledStaticCount = await chrome.declarativeNetRequest.getEnabledRulesets();

  // Compare rule counts to determine if anything needs to be disabled so that
  // new rules can be enabled
  const proposedCount = enableRulesetIds.length;
  if (enabledStaticCount + proposedCount > chrome.declarativeNetRequest.MAX_NUMBER_OF_ENABLED_STATIC_RULESETS) {
    options.disableRulesetIds = disableCandidateIds
  }

  // Update the enabled static rules
  await chrome.declarativeNetRequest.updateEnabledRulesets(options);
}
```

===

---
title: chrome.desktopCapture
url: https://developer.chrome.com/docs/extensions/reference/api/desktopCapture
---

## Description

The Desktop Capture API captures the content of the screen, individual windows, or individual tabs.

## Permissions

`desktopCapture`

## Types

### DesktopCaptureSourceType

Enum used to define set of desktop media sources used in `chooseDesktopMedia()`.

#### Enum

`"screen"`

`"window"`

`"tab"`

`"audio"`

### SelfCapturePreferenceEnum

Chrome 107+

Mirrors `SelfCapturePreferenceEnum`.

#### Enum

`"include"`

`"exclude"`

### SystemAudioPreferenceEnum

Chrome 105+

Mirrors `SystemAudioPreferenceEnum`.

#### Enum

`"include"`

`"exclude"`

## Methods

### cancelChooseDesktopMedia()

```javascript
chrome.desktopCapture.cancelChooseDesktopMedia(
  desktopMediaRequestId: number,
)
```

Hides desktop media picker dialog shown by `chooseDesktopMedia()`.

#### Parameters

*   `desktopMediaRequestId`

    `number`

    Id returned by `chooseDesktopMedia()`

### chooseDesktopMedia()

```javascript
chrome.desktopCapture.chooseDesktopMedia(
  sources: DesktopCaptureSourceType[],
  targetTab?: Tab,
  callback: function,
)
```

Shows desktop media picker UI with the specified set of sources.

#### Parameters

*   `sources`

    `DesktopCaptureSourceType[]`

    Set of sources that should be shown to the user. The sources order in the set decides the tab order in the picker.
*   `targetTab`

    `Tab` optional

    Optional tab for which the stream is created. If not specified then the resulting stream can be used only by the calling extension. The stream can only be used by frames in the given tab whose security origin matches `tab.url`. The tab's origin must be a secure origin, e.g. HTTPS.
*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (streamId: string, options: object) => void
    ```

    *   `streamId`

        `string`

        An opaque string that can be passed to `getUserMedia()` API to generate media stream that corresponds to the source selected by the user. If user didn't select any source (i.e. canceled the prompt) then the callback is called with an empty `streamId`. The created `streamId` can be used only once and expires after a few seconds when it is not used.
    *   `options`

        `object`

        Chrome 57+

        Contains properties that describe the stream.

        *   `canRequestAudioTrack`

            `boolean`

            True if `"audio"` is included in parameter `sources`, and the end user does not uncheck the `"Share audio"` checkbox. Otherwise `false`, and in this case, one should not ask for audio stream through `getUserMedia` call.

#### Returns

*   `number`

    An id that can be passed to `cancelChooseDesktopMedia()` in case the prompt need to be canceled.

===

---
title: chrome.devtools.inspectedWindow
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/inspectedWindow
---

## Description

Use the `chrome.devtools.inspectedWindow` API to interact with the inspected window: obtain the tab ID for the inspected page, evaluate the code in the context of the inspected window, reload the page, or obtain the list of resources within the page.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

The `tabId` property provides the tab identifier that you can use with the `chrome.tabs.*` API calls. However, please note that `chrome.tabs.*` API is not exposed to the Developer Tools extension pages due to security considerations鈥攜ou will need to pass the tab ID to the background page and invoke the `chrome.tabs.*` API functions from there.

The `reload` method may be used to reload the inspected page. Additionally, the caller can specify an override for the user agent string, a script that will be injected early upon page load, or an option to force reload of cached resources.

Use the `getResources` call and the `onResourceContent` event to obtain the list of resources (documents, stylesheets, scripts, images etc) within the inspected page. The `getContent` and `setContent` methods of the `Resource` class along with the `onResourceContentCommitted` event may be used to support modification of the resource content, for example, by an external editor.

## Manifest

The following keys must be declared in the manifest to use this API.

`"devtools_page"`

## Execute code in the inspected window

The `eval` method provides the ability for extensions to execute JavaScript code in the context of the inspected page. This method is powerful when used in the right context and dangerous when used inappropriately. Use the `tabs.executeScript` method unless you need the specific functionality that the `eval` method provides.

Here are the main differences between the `eval` and `tabs.executeScript` methods:

*   The `eval` method does not use an isolated world for the code being evaluated, so the JavaScript state of the inspected window is accessible to the code. Use this method when access to the JavaScript state of the inspected page is required.
*   The execution context of the code being evaluated includes the Developer Tools console API. For example, the code can use `inspect` and `$0`.
*   The evaluated code may return a value that is passed to the extension callback. The returned value has to be a valid JSON object (it may contain only primitive JavaScript types and acyclic references to other JSON objects). Please observe extra care while processing the data received from the inspected page鈥攖he execution context is essentially controlled by the inspected page; a malicious page may affect the data being returned to the extension.

Caution: Due to the security considerations explained above, the `scripting.executeScript` method is the preferred way for an extension to access DOM data of the inspected page in cases where the access to JavaScript state of the inspected page is not required.

Note that a page can include multiple different JavaScript execution contexts. Each frame has its own context, plus an additional context for each extension that has content scripts running in that frame.

By default, the `eval` method executes in the context of the main frame of the inspected page.

The `eval` method takes an optional second argument that you can use to specify the context in which the code is evaluated. This options object can contain one or more of the following keys:

`frameURL`
:   Use to specify a frame other than the inspected page's main frame.

`contextSecurityOrigin`
:   Use to select a context within the specified frame according to its web origin.

`useContentScriptContext`
:   If `true`, execute the script in the same context as the extensions's content scripts. (Equivalent to specifying the extensions's own web orgin as the context security origin.) This can be used to exchange data with the content script.

## Examples

The following code checks for the version of jQuery used by the inspected page:

```javascript
chrome.devtools.inspectedWindow.eval(
  "jQuery.fn.jquery",
  function(result, isException) {
    if (isException) {
      console.log("the page is not using jQuery");
    } else {
      console.log("The page is using jQuery v" + result);
    }
  }
);
```

To try this API, install the devtools API examples from the `chrome-extension-samples` repository.

## Types

### Resource

A resource within the inspected page, such as a document, a script, or an image.

#### Properties

*   `url`

    `string`

    The URL of the resource.
*   `getContent`

    `void`

    Gets the content of the resource.

    The `getContent` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        (content: string, encoding: string) => void
        ```

        *   `content`

            `string`

            Content of the resource (potentially encoded).
        *   `encoding`

            `string`

            Empty if the content is not encoded, encoding name otherwise. Currently, only `base64` is supported.
*   `setContent`

    `void`

    Sets the content of the resource.

    The `setContent` function looks like:

    ```javascript
    (content: string, commit: boolean, callback?: function) => {...}
    ```

    *   `content`

        `string`

        New content of the resource. Only resources with the text type are currently supported.
    *   `commit`

        `boolean`

        `True` if the user has finished editing the resource, and the new content of the resource should be persisted; `false` if this is a minor change sent in progress of the user editing the resource.
    *   `callback`

        `function` optional

        The callback parameter looks like:

        ```javascript
        (error?: object) => void
        ```

        *   `error`

            `object` optional

            Set to `undefined` if the resource content was set successfully; describes error otherwise.

## Properties

### tabId

The ID of the tab being inspected. This ID may be used with `chrome.tabs.*` API.

#### Type

`number`

## Methods

### eval()

```javascript
chrome.devtools.inspectedWindow.eval(
  expression: string,
  options?: object,
  callback?: function,
)
```

Evaluates a JavaScript expression in the context of the main frame of the inspected page. The expression must evaluate to a JSON-compliant object, otherwise an exception is thrown. The `eval` function can report either a DevTools-side error or a JavaScript exception that occurs during evaluation. In either case, the `result` parameter of the callback is `undefined`. In the case of a DevTools-side error, the `isException` parameter is non-null and has `isError` set to `true` and `code` set to an error code. In the case of a JavaScript error, `isException` is set to `true` and `value` is set to the string value of thrown object.

#### Parameters

*   `expression`

    `string`

    An expression to evaluate.
*   `options`

    `object` optional

    The options parameter can contain one or more options.

    *   `frameURL`

        `string` optional

        If specified, the expression is evaluated on the iframe whose URL matches the one specified. By default, the expression is evaluated in the top frame of the inspected page.
    *   `scriptExecutionContext`

        `string` optional

        Chrome 107+

        Evaluate the expression in the context of a content script of an extension that matches the specified origin. If given, `scriptExecutionContext` overrides the '`true`' setting on `useContentScriptContext`.
    *   `useContentScriptContext`

        `boolean` optional

        Evaluate the expression in the context of the content script of the calling extension, provided that the content script is already injected into the inspected page. If not, the expression is not evaluated and the callback is invoked with the exception parameter set to an object that has the `isError` field set to `true` and the `code` field set to `E_NOTFOUND`.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (result: object, exceptionInfo: object) => void
    ```

    *   `result`

        `object`

        The result of evaluation.
    *   `exceptionInfo`

        `object`

        An object providing details if an exception occurred while evaluating the expression.

        *   `code`

            `string`

            Set if the error occurred on the DevTools side before the expression is evaluated.
        *   `description`

            `string`

            Set if the error occurred on the DevTools side before the expression is evaluated.
        *   `details`

            `any[]`

            Set if the error occurred on the DevTools side before the expression is evaluated, contains the array of the values that may be substituted into the description string to provide more information about the cause of the error.
        *   `isError`

            `boolean`

            Set if the error occurred on the DevTools side before the expression is evaluated.
        *   `isException`

            `boolean`

            Set if the evaluated code produces an unhandled exception.
        *   `value`

            `string`

            Set if the evaluated code produces an unhandled exception.

### getResources()

```javascript
chrome.devtools.inspectedWindow.getResources(
  callback: function,
)
```

Retrieves the list of resources from the inspected page.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (resources: Resource[]) => void
    ```

    *   `resources`

        `Resource[]`

        The resources within the page.

### reload()

```javascript
chrome.devtools.inspectedWindow.reload(
  reloadOptions?: object,
)
```

Reloads the inspected page.

#### Parameters

*   `reloadOptions`

    `object` optional

    *   `ignoreCache`

        `boolean` optional

        When `true`, the loader will bypass the cache for all inspected page resources loaded before the `load` event is fired. The effect is similar to pressing Ctrl+Shift+R in the inspected window or within the Developer Tools window.
    *   `injectedScript`

        `string` optional

        If specified, the script will be injected into every frame of the inspected page immediately upon load, before any of the frame's scripts. The script will not be injected after subsequent reloads鈥攆or example, if the user presses Ctrl+R.
    *   `userAgent`

        `string` optional

        If specified, the string will override the value of the `User-Agent` HTTP header that's sent while loading the resources of the inspected page. The string will also override the value of the `navigator.userAgent` property that's returned to any scripts that are running within the inspected page.

## Events

### onResourceAdded

```javascript
chrome.devtools.inspectedWindow.onResourceAdded.addListener(
  callback: function,
)
```

Fired when a new resource is added to the inspected page.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (resource: Resource) => void
    ```

    *   `resource`

        `Resource`

### onResourceContentCommitted

```javascript
chrome.devtools.inspectedWindow.onResourceContentCommitted.addListener(
  callback: function,
)
```

Fired when a new revision of the resource is committed (e.g. user saves an edited version of the resource in the Developer Tools).

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (resource: Resource, content: string) => void
    ```

    *   `resource`

        `Resource`
    *   `content`

        `string`

===

---
title: chrome.devtools.network
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/network
---

## Description

Use the `chrome.devtools.network` API to retrieve the information about network requests displayed by the Developer Tools in the Network panel.

Network requests information is represented in the HTTP Archive format (HAR). The description of HAR is outside of scope of this document, refer to HAR v1.2 Specification.

In terms of HAR, the `chrome.devtools.network.getHAR()` method returns entire HAR log, while `chrome.devtools.network.onRequestFinished` event provides HAR entry as an argument to the event callback.

Note that request content is not provided as part of HAR for efficiency reasons. You may call request's `getContent()` method to retrieve content.

If the Developer Tools window is opened after the page is loaded, some requests may be missing in the array of entries returned by `getHAR()`. Reload the page to get all requests. In general, the list of requests returned by `getHAR()` should match that displayed in the Network panel.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

## Manifest

The following keys must be declared in the manifest to use this API.

`"devtools_page"`

## Examples

The following code logs URLs of all images larger than 40KB as they are loaded:

```javascript
chrome.devtools.network.onRequestFinished.addListener(
  function(request) {
    if (request.response.bodySize > 40*1024) {
      chrome.devtools.inspectedWindow.eval(
        'console.log("Large image: " + unescape("' + escape(request.request.url) + '"))');
    }
  }
);
```

To try this API, install the devtools API examples from the `chrome-extension-samples` repository.

## Types

### Request

Represents a network request for a document resource (script, image and so on). See HAR Specification for reference.

#### Properties

*   `getContent`

    `void`

    Returns content of the response body.

    The `getContent` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        (content: string, encoding: string) => void
        ```

        *   `content`

            `string`

            Content of the response body (potentially encoded).
        *   `encoding`

            `string`

            Empty if content is not encoded, encoding name otherwise. Currently, only `base64` is supported.

## Methods

### getHAR()

```javascript
chrome.devtools.network.getHAR(
  callback: function,
)
```

Returns HAR log that contains all known network requests.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (harLog: object) => void
    ```

    *   `harLog`

        `object`

        A HAR log. See HAR specification for details.

## Events

### onNavigated

```javascript
chrome.devtools.network.onNavigated.addListener(
  callback: function,
)
```

Fired when the inspected window navigates to a new page.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (url: string) => void
    ```

    *   `url`

        `string`

### onRequestFinished

```javascript
chrome.devtools.network.onRequestFinished.addListener(
  callback: function,
)
```

Fired when a network request is finished and all request data are available.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    (request: Request) => void
    ```

    *   `request`

        `Request`

===

---
title: chrome.devtools.panels
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/panels
---

## Description

Use the `chrome.devtools.panels` API to integrate your extension into Developer Tools window UI: create your own panels, access existing panels, and add sidebars.

Each extension panel and sidebar is displayed as a separate HTML page. All extension pages displayed in the Developer Tools window have access to all parts of the `chrome.devtools` API, as well as all other extension APIs.

You can use the `devtools.panels.setOpenResourceHandler` method to install a callback function that handles user requests to open a resource (typically, a click a resource link in the Developer Tools window). At most one of the installed handlers gets called; users can specify (using the Developer Tools Settings dialog) either the default behavior or an extension to handle resource open requests. If an extension calls `setOpenResourceHandler()` multiple times, only the last handler is retained.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

## Manifest

The following keys must be declared in the manifest to use this API.

`"devtools_page"`

## Example

The following code adds a panel contained in `Panel.html`, represented by `FontPicker.png` on the Developer Tools toolbar and labeled as `Font Picker`:

```javascript
chrome.devtools.panels.create("Font Picker", "FontPicker.png", "Panel.html", function(panel) { ... });
```

The following code adds a sidebar pane contained in `Sidebar.html` and titled `Font Properties` to the Elements panel, then sets its height to `8ex`:

```javascript
chrome.devtools.panels.elements.createSidebarPane("Font Properties", function(sidebar) { sidebar.setPage("Sidebar.html"); sidebar.setHeight("8ex"); } );
```

The screenshot illustrates the effect this example would have on Developer Tools window:

Extension icon panel on DevTools toolbar.

To try this API, install the devtools panels API example from the `chrome-extension-samples` repository.

## Types

### Button

A button created by the extension.

#### Properties

*   `onClicked`

    `Event<functionvoidvoid>`

    Fired when the button is clicked.

    The `onClicked.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `update`

    `void`

    Updates the attributes of the button. If some of the arguments are omitted or `null`, the corresponding attributes are not updated.

    The `update` function looks like:

    ```javascript
    (iconPath?: string, tooltipText?: string, disabled?: boolean) => {...}
    ```

    *   `iconPath`

        `string` optional

        Path to the new icon of the button.
    *   `tooltipText`

        `string` optional

        Text shown as a tooltip when user hovers the mouse over the button.
    *   `disabled`

        `boolean` optional

        Whether the button is disabled.

### ElementsPanel

Represents the Elements panel.

#### Properties

*   `onSelectionChanged`

    `Event<functionvoidvoid>`

    Fired when an object is selected in the panel.

    The `onSelectionChanged.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `createSidebarPane`

    `void`

    Creates a pane within panel's sidebar.

    The `createSidebarPane` function looks like:

    ```javascript
    (title: chrome.string, callback?: function) => {...}
    ```

    *   `title`

        `string`

        Text that is displayed in sidebar caption.
    *   `callback`

        `function` optional

        The callback parameter looks like:

        ```javascript
        (result: ExtensionSidebarPane) => void
        ```

        *   `result`

            `ExtensionSidebarPane`

            An `ExtensionSidebarPane` object for created sidebar pane.

### ExtensionPanel

Represents a panel created by extension.

#### Properties

*   `onHidden`

    `Event<functionvoidvoid>`

    Fired when the user switches away from the panel.

    The `onHidden.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `onSearch`

    `Event<functionvoidvoid>`

    Fired upon a search action (start of a new search, search result navigation, or search being canceled).

    The `onSearch.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        (action: string, queryString?: string) => void
        ```

        *   `action`

            `string`
        *   `queryString`

            `string` optional
*   `onShown`

    `Event<functionvoidvoid>`

    Fired when the user switches to the panel.

    The `onShown.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        (window: Window) => void
        ```

        *   `window`

            `Window`
*   `createStatusBarButton`

    `void`

    Appends a button to the status bar of the panel.

    The `createStatusBarButton` function looks like:

    ```javascript
    (iconPath: string, tooltipText: string, disabled: boolean) => {...}
    ```

    *   `iconPath`

        `string`

        Path to the icon of the button. The file should contain a 64x24-pixel image composed of two 32x24 icons. The left icon is used when the button is inactive; the right icon is displayed when the button is pressed.
    *   `tooltipText`

        `string`

        Text shown as a tooltip when user hovers the mouse over the button.
    *   `disabled`

        `boolean`

        Whether the button is disabled.

    *   returns

        `Button`

### ExtensionSidebarPane

A sidebar created by the extension.

#### Properties

*   `onHidden`

    `Event<functionvoidvoid>`

    Fired when the sidebar pane becomes hidden as a result of the user switching away from the panel that hosts the sidebar pane.

    The `onHidden.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `onShown`

    `Event<functionvoidvoid>`

    Fired when the sidebar pane becomes visible as a result of user switching to the panel that hosts it.

    The `onShown.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        (window: Window) => void
        ```

        *   `window`

            `Window`
*   `setExpression`

    `void`

    Sets an expression that is evaluated within the inspected page. The result is displayed in the sidebar pane.

    The `setExpression` function looks like:

    ```javascript
    (expression: string, rootTitle?: string, callback?: function) => {...}
    ```

    *   `expression`

        `string`

        An expression to be evaluated in context of the inspected page. JavaScript objects and DOM nodes are displayed in an expandable tree similar to the console/watch.
    *   `rootTitle`

        `string` optional

        An optional title for the root of the expression tree.
    *   `callback`

        `function` optional

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `setHeight`

    `void`

    Sets the height of the sidebar.

    The `setHeight` function looks like:

    ```javascript
    (height: string) => {...}
    ```

    *   `height`

        `string`

        A CSS-like size specification, such as '`100px`' or '`12ex`'.
*   `setObject`

    `void`

    Sets a JSON-compliant object to be displayed in the sidebar pane.

    The `setObject` function looks like:

    ```javascript
    (jsonObject: string, rootTitle?: string, callback?: function) => {...}
    ```

    *   `jsonObject`

        `string`

        An object to be displayed in context of the inspected page. Evaluated in the context of the caller (API client).
    *   `rootTitle`

        `string` optional

        An optional title for the root of the expression tree.
    *   `callback`

        `function` optional

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `setPage`

    `void`

    Sets an HTML page to be displayed in the sidebar pane.

    The `setPage` function looks like:

    ```javascript
    (path: string) => {...}
    ```

    *   `path`

        `string`

        Relative path of an extension page to display within the sidebar.

### SourcesPanel

Represents the Sources panel.

#### Properties

*   `onSelectionChanged`

    `Event<functionvoidvoid>`

    Fired when an object is selected in the panel.

    The `onSelectionChanged.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `createSidebarPane`

    `void`

    Creates a pane within panel's sidebar.

    The `createSidebarPane` function looks like:

    ```javascript
    (title: chrome.string, callback?: function) => {...}
    ```

    *   `title`

        `string`

        Text that is displayed in sidebar caption.
    *   `callback`

        `function` optional

        The callback parameter looks like:

        ```javascript
        (result: ExtensionSidebarPane) => void
        ```

        *   `result`

            `ExtensionSidebarPane`

            An `ExtensionSidebarPane` object for created sidebar pane.

## Properties

### elements

Elements panel.

#### Type

`ElementsPanel`

### sources

Sources panel.

#### Type

`SourcesPanel`

### themeName

Chrome 59+

The name of the color theme set in user's DevTools settings. Possible values: `default` (the default) and `dark`.

#### Type

`string`

## Methods

### create()

```javascript
chrome.devtools.panels.create(
  title: chrome.string,
  iconPath: string,
  pagePath: string,
  callback?: function,
)
```

Creates an extension panel.

#### Parameters

*   `title`

    `string`

    Title that is displayed next to the extension icon in the Developer Tools toolbar.
*   `iconPath`

    `string`

    Path of the panel's icon relative to the extension directory.
*   `pagePath`

    `string`

    Path of the panel's HTML page relative to the extension directory.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (panel: ExtensionPanel) => void
    ```

    *   `panel`

        `ExtensionPanel`

        An `ExtensionPanel` object representing the created panel.

### openResource()

```javascript
chrome.devtools.panels.openResource(
  url: string,
  lineNumber: number,
  columnNumber?: number,
  callback?: function,
)
```

Requests DevTools to open a URL in a Developer Tools panel.

#### Parameters

*   `url`

    `string`

    The URL of the resource to open.
*   `lineNumber`

    `number`

    Specifies the line number to scroll to when the resource is loaded.
*   `columnNumber`

    `number` optional

    Chrome 114+

    Specifies the column number to scroll to when the resource is loaded.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

### setOpenResourceHandler()

```javascript
chrome.devtools.panels.setOpenResourceHandler(
  callback?: function,
)
```

Specifies the function to be called when the user clicks a resource link in the Developer Tools window. To unset the handler, either call the method with no parameters or pass `null` as the parameter.

#### Parameters

*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (resource: Resource, lineNumber: number) => void
    ```

    *   `resource`

        `Resource`

        A `devtools.inspectedWindow.Resource` object for the resource that was clicked.
    *   `lineNumber`

        `number`

        Pending

        Specifies the line number within the resource that was clicked.

===

---
title: chrome.devtools.performance
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/performance
---

## Description

Use the `chrome.devtools.performance` API to listen to recording status updates in the Performance panel in DevTools.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

## Availability

Chrome 129+

Starting from Chrome 128, you can listen to notifications of the recording status of the Performance panel.

## Concepts and usage

The `chrome.devtools.performance` API allows developers to interact with the recording features of the Performance panel panel in Chrome DevTools. You can use this API to get notifications when recording starts or stops.

Two events are available:

*   `onProfilingStarted`: This event is fired when the Performance panel begins recording performance data.
*   `onProfilingStopped`: This event is fired when the Performance panel stops recording performance data.

Both events don't have any associated parameters.

By listening to these events, developers can create extensions that react to the recording status in the Performance panel, providing additional automation during performance profiling.

## Examples

This is how you can use the API to listen to recording status updates

```javascript
chrome.devtools.performance.onProfilingStarted.addListener(() => {
  // Profiling started listener implementation
});
chrome.devtools.performance.onProfilingStopped.addListener(() => {
  // Profiling stopped listener implementation
})
```

## Events

### onProfilingStarted

```javascript
chrome.devtools.performance.onProfilingStarted.addListener(
  callback: function,
)
```

Fired when the Performance panel starts recording.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    () => void
    ```

### onProfilingStopped

```javascript
chrome.devtools.performance.onProfilingStopped.addListener(
  callback: function,
)
```

Fired when the Performance panel stops recording.

#### Parameters

*   `callback`

    `function`

    The callback parameter looks like:

    ```javascript
    () => void
    ```

===

---
title: chrome.devtools.recorder
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/recorder
---

## Description

Use the `chrome.devtools.recorder` API to customize the Recorder panel in DevTools.

`devtools.recorder` API is a preview feature that allows you to extend the Recorder panel in Chrome DevTools.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

## Availability

Chrome 105+

Starting from Chrome 105, you can extend the export functionality. Starting from Chrome 112, you can extend the replay button.

## Concepts and usage

### Customizing the export feature

To register an extension plugin, use the `registerRecorderExtensionPlugin` function. This function requires a plugin instance, a `name` and a `mediaType` as parameters. The plugin instance must implement two methods: `stringify` and `stringifyStep`.

The `name` provided by the extension shows up in the Export menu in the Recorder panel.

Depending on the export context, when the user clicks the export option provided by the extension, the Recorder panel invokes one of the two functions:

*   `stringify` that receives an entire user flow recording
*   `stringifyStep` that receives a single recorded step

The `mediaType` parameter allows the extension to specify the kind of output it generates with the `stringify` and `stringifyStep` functions. For example, `application/javascript` if the result is a JavaScript program.

### Customizing the replay button

To customize the replay button in the Recorder, use the `registerRecorderExtensionPlugin` function. The plugin must implement the `replay` method for the customization to take effect. If the method is detected, a replay button will appear in the Recorder. Upon clicking the button, the current recording object will be passed as the first argument to the `replay` method.

At this point, the extension can display a `RecorderView` for handling the replay or use other extension APIs to process the replay request. To create a new `RecorderView`, invoke `chrome.devtools.recorder.createView`.

## Examples

### Export plugin

The following code implements an extension plugin that stringifes a recording using `JSON.stringify`:

```javascript
class MyPlugin {
  stringify(recording) {
    return Promise.resolve(JSON.stringify(recording));
  }
  stringifyStep(step) {
    return Promise.resolve(JSON.stringify(step));
  }
}
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  new MyPlugin(),
  /*name=*/'MyPlugin',
  /*mediaType=*/'application/json'
);
```

### Replay plugin

The following code implements an extension plugin that creates a dummy Recorder view and displays it upon a replay request:

```javascript
const view = await chrome.devtools.recorder.createView(
  /* name= */ 'ExtensionName',
  /* pagePath= */ 'Replay.html'
);
let latestRecording;
view.onShown.addListener(() => {
  // Recorder has shown the view. Send additional data to the view if needed.
  chrome.runtime.sendMessage(JSON.stringify(latestRecording));
});
view.onHidden.addListener(() => {
  // Recorder has hidden the view.
});
export class RecorderPlugin {
  replay(recording) {
    // Share the data with the view.
    latestRecording = recording;
    // Request to show the view.
    view.show();
  }
}
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  new RecorderPlugin(),
  /* name=*/ 'CoffeeTest'
);
```

Find a complete extension example on GitHub.

## Types

### RecorderExtensionPlugin

A plugin interface that the Recorder panel invokes to customize the Recorder panel.

#### Properties

*   `replay`

    `void`

    Chrome 112+

    Allows the extension to implement custom replay functionality.

    The `replay` function looks like:

    ```javascript
    (recording: object) => {...}
    ```

    *   `recording`

        `object`

        A recording of the user interaction with the page. This should match Puppeteer's recording schema.
*   `stringify`

    `void`

    Converts a recording from the Recorder panel format into a string.

    The `stringify` function looks like:

    ```javascript
    (recording: object) => {...}
    ```

    *   `recording`

        `object`

        A recording of the user interaction with the page. This should match Puppeteer's recording schema.
*   `stringifyStep`

    `void`

    Converts a step of the recording from the Recorder panel format into a string.

    The `stringifyStep` function looks like:

    ```javascript
    (step: object) => {...}
    ```

    *   `step`

        `object`

        A step of the recording of a user interaction with the page. This should match Puppeteer's step schema.

### RecorderView

Chrome 112+

Represents a view created by extension to be embedded inside the Recorder panel.

#### Properties

*   `onHidden`

    `Event<functionvoidvoid>`

    Fired when the view is hidden.

    The `onHidden.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `onShown`

    `Event<functionvoidvoid>`

    Fired when the view is shown.

    The `onShown.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `show`

    `void`

    Indicates that the extension wants to show this view in the Recorder panel.

    The `show` function looks like:

    ```javascript
    () => {...}
    ```

## Methods

### createView()

Chrome 112+

```javascript
chrome.devtools.recorder.createView(
  title: chrome.string,
  pagePath: string,
)
```

Creates a view that can handle the replay. This view will be embedded inside the Recorder panel.

#### Parameters

*   `title`

    `string`

    Title that is displayed next to the extension icon in the Developer Tools toolbar.
*   `pagePath`

    `string`

    Path of the panel's HTML page relative to the extension directory.

#### Returns

*   `RecorderView`

### registerRecorderExtensionPlugin()

```javascript
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  plugin: RecorderExtensionPlugin,
  name: string,
  mediaType: string,
)
```

Registers a Recorder extension plugin.

#### Parameters

*   `plugin`

    `RecorderExtensionPlugin`

    An instance implementing the `RecorderExtensionPlugin` interface.
*   `name`

    `string`

    The name of the plugin.
*   `mediaType`

    `string`

    The media type of the string content that the plugin produces.

===

---
title: chrome.dns
url: https://developer.chrome.com/docs/extensions/reference/api/dns
---

## Description

Use the `chrome.dns` API for dns resolution.

## Permissions

`dns`

## Availability

Dev channel

To use this API, you must declare the `"dns"` permission in the manifest.

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "dns"
  ],
  ...
}
```

Note: This API is only available in Chrome Dev. There are no foreseeable plans to move this API from the dev channel into Chrome stable.

## Usage

The following code calls `resolve()` to retrieve the IP address of `example.com`.

service-worker.js:

```javascript
const resolveDNS = async () => {
  let record = await chrome.dns.resolve('example.com');
  console.log(record.address); // "192.0.2.172"
};
resolveDNS();
```

Key point: Do not include the scheme or trailing slash in the hostname. For example, `https://example.com/` is invalid.

## Types

### ResolveCallbackResolveInfo

#### Properties

*   `address`

    `string` optional

    A string representing the IP address literal. Supplied only if `resultCode` indicates success.
*   `resultCode`

    `number`

    The result code. Zero indicates success.

## Methods

### resolve()

Promise

```javascript
chrome.dns.resolve(
  hostname: string,
  callback?: function,
)
```

Resolves the given hostname or IP address literal.

#### Parameters

*   `hostname`

    `string`

    The hostname to resolve.
*   `callback`

    `function` optional

    The callback parameter looks like:

    ```javascript
    (resolveInfo: ResolveCallbackResolveInfo) => void
    ```

    *   `resolveInfo`

        `ResolveCallbackResolveInfo`

#### Returns

*   `Promise<ResolveCallbackResolveInfo>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

===

---
title: chrome.documentScan
url: https://developer.chrome.com/docs/extensions/reference/api/documentScan
---

## Description

Use the `chrome.documentScan` API to discover and retrieve images from attached document scanners.

The Document Scan API is designed to allow apps and extensions to view the content of paper documents on an attached document scanner.

**Important:** This API works only on ChromeOS.

## Permissions

`documentScan`

## Availability

Chrome 44+ ChromeOS only

Availability for API members added later is shown with those members.

## Concepts and usage

This API supports two means of scanning documents. If your use case can work with any scanner and doesn't require control of the configuration, use the `scan()` method. More complicated use cases require a combination of methods, which are only supported in Chrome 124 and later.

### Simple scanning

For simple use cases, meaning those that can work with any scanner and don't require control of configuration, call `scan()`. This method takes a `ScanOptions` object and returns a `Promise` that resolves with a `ScanResults` object. The capabilities of this option are limited to the number of scans and the MIME types that will be accepted by the caller. Scans are returned as URLs for display in an `<img>` tag for a user interface.

### Complex scanning

Complex scans are accomplished in three phases as described in this section. This outline does not describe every method argument or every property returned in a response. It is only intended to give you a general guide to writing scanner code.

**Note:** Calling `openScanner()`, `getScannerList()`, or `startScan()` more than once will cancel operations initiated by previous calls to these methods. See the descriptions of these methods for specifics.

#### Discovery

1.  Call `getScannerList()`. Available scanners are returned in a `Promise` that resolves with a `GetScannerListResponse`.
    *   The response object contains an array of `ScannerInfo` objects.
    *   The array may contain multiple entries for a single scanner if that scanner supports multiple protocols or connection methods.
2.  Select a scanner from the returned array and save the value of its `scannerId` property.
    Use the properties of individual `ScannerInfo` objects to distinguish among multiple objects for the same scanner. Objects from the same scanner will have the same value for the `deviceUuid` property. `ScannerInfo` also contains an `imageFormats` property containing an array of supported image types.

#### Scanner configuration

1.  Call `openScanner()`, passing in the saved scanner ID. It returns a `Promise` that resolves with an `OpenScannerResponse`. The response object contains:
    *   A `scannerHandle` property, which you'll need to save.
    *   An `options` property containing scanner-specific properties, which you'll need to set. See Retrieve scanner options for more information.
2.  (Optional) If you need the user to provide values for scanner options, construct a user interface. You will need the scanner options provided by the previous step, and you'll need to retrieve option groups provided by the scanner. See Construct a user interface for more information.
3.  Construct an array of `OptionSetting` objects using programmatic or user-provided values. See Set scanner options for more information.
4.  Pass the array of `OptionSetting` objects to `setOptions()` to set options for the scanner. It returns a `Promise` that resolves with a `SetOptionsResponse`. This object contains an updated version of the scanner options retrieved in step 1 of scanner configuration.
    Since changing one option can alter constraints on another option, you may need to repeat these steps several times.

#### Scanning

1.  Construct a `StartScanOptions` object and pass it to `startScan()`. It returns a `Promise` that resolves with a `StartScanResponse`. Its `job` property is a handle that you will use to either read scan data or cancel the scan.
2.  Pass the job handle to `readScanData()`. It returns a `Promise` that resolves with a `ReadScanDataResponse` object. If data was read successfully, its `result` property equals `SUCCESS` and its `data` property contains an `ArrayBuffer` with part of the scan. Note that `estimatedCompletion` contains an estimated percentage of the total data that has been delivered so far.
    **Note:** If `result` is `SUCCESS`, but `data` is empty, delay briefly before calling `readScanData()` again.
3.  Repeat the previous step until the `result` property equals `EOF` or an error.

When the end of the scan is reached, call `closeScanner()` with the scanner handle saved in step 3. It returns a `Promise` that resolves with a `CloseScannerResponse`. Calling `cancelScan()` at any time after the job is created will end scanning.

### Response objects

All methods return a `Promise` that resolves with a response object of some kind. Most of these contain a `result` property whose value is a member of `OperationResult`. Some properties of response objects won't contain values unless the value of `result` has a specific value. These relationships are described in the reference for each response object.

For example, `OpenScannerResponse.scannerHandle` will only have a value when `OpenScannerResponse.result` equals `SUCCESS`.

### Scanner options

Scanner options vary considerably by device. Consequently, it's not possible to reflect scanner options directly within the `documentScan` API. To get around this, the `OpenScannerResponse` (retrieved using `openScanner()`) and the `SetOptionsResponse` (the response object for `setOptions()`) contain an `options` property which is an object containing scanner-specific options. Each option is a key-value mapping where the key is a device-specific option and the value is an instance of `ScannerOption`.

The structure generally looks like this:

```
{ "key1": { scannerOptionInstance } "key2": { scannerOptionInstance } }
```

For example, imagine a scanner that returns options named `"source"` and `"resolution"`. The structure of the returned `options` object will look something like the following example. For simplicity, only partial `ScannerOption` responses are shown.

```
{ "source": { "name": "source", "type": OptionType.STRING, ... }, "resolution": { "name": "resolution", "type": OptionType.INT, ... }, ... }
```

### Construct a user interface

Though not required to use this API, you may want a user to choose the value for a particular option. This requires a user interface. Use the `OpenScannerResponse` (opened by `openScanner()`) to retrieve the options for the attached scanner as described in the previous section.

Some scanners group options in device-specific ways. They don't affect option behaviors, but since these groups may be mentioned in a scanner's product documentation, such groups should be shown to the user. You can retrieve these groups by calling `getOptionGroups()`. This returns a `Promise` that resolves with a `GetOptionGroupsResponse` object. Its `groups` property contains a scanner-specific array of groups. Use the information in these groups to organize the options in the `OpenScannerResponse` for display.

```
{ scannerHandle: "123456", result: SUCCESS, groups: [ { title: chrome."Standard", members: [ "resolution", "mode", "source" ] } ] }
```

As stated under Scanner configuration, changing one option can alter constraints on another option. This is why `setOptionsResponse` (the response object for `setOptions()`) contains another `options` property. Use this to update the user interface. Then repeat as needed until all options are set.

### Set scanner options

Set scanner options by passing an array of `OptionSetting` objects to `setOptions()`. For an example, see the following Scan one letter-size page section.

## Examples

### Retrieve a page as a blob

This example shows one way to retrieve a page from the scanner as a blob and demonstrates use of `startScan()` and `readScanData()` using the value of `OperationResult`.

```javascript
async function pageAsBlob(handle) {
  let response = await chrome.documentScan.startScan(
    handle,
    {format: "image/jpeg"});
  if (response.result != chrome.documentScan.OperationResult.SUCCESS) {
    return null;
  }
  const job = response.job;
  let imgParts = [];
  response = await chrome.documentScan.readScanData(job);
  while (response.result == chrome.documentScan.OperationResult.SUCCESS) {
    if (response.data && response.data.byteLength > 0) {
      imgParts.push(response.data);
    } else {
      // Delay so hardware can make progress.
      await new Promise(r => setTimeout(r, 100));
    }
    response = await chrome.documentScan.readScanData(job);
  }
  if (response.result != chrome.documentScan.OperationResult.EOF) {
    return null;
  }
  if (response.data && response.data.byteLength > 0) {
    imgParts.push(response.data);
  }
  return new Blob(imgParts, { type: "image/jpeg" });
}
```

### Scan one letter-size page

This example shows how to select a scanner, set its options, and open it. It then retrieves the contents of a single page and closes the scanner. This process demonstrates using `getScannerList()`, `openScanner()`, `setOptions()`, and `closeScanner()`. Note that the contents of the page are retrieved by calling the `pageAsBlob()` function from the previous example.

```javascript
async function scan() {
  let response = await chrome.documentScan.getScannerList({ secure: true });
  let scanner = await chrome.documentScan.openScanner(
    response.scanners[0].scannerId);
  const handle = scanner.scannerHandle;
  let options = [];
  for (source of scanner.options["source"].constraint.list) {
    if (source.includes("ADF")) {
      options.push({
        name: "source",
        type: chrome.documentScan.OptionType.STRING,
        value: { value: source }
      });
      break;
    }
  }
  options.push({
    name: "tl-x",
    type: chrome.documentScan.OptionType.FIXED,
    value: 0.0
  });
  options.push({
    name: "br-x",
    type: chrome.documentScan.OptionType.FIXED,
    value: 215.9 // 8.5" in mm
  });
  options.push({
    name: "tl-y",
    type: chrome.documentScan.OptionType.FIXED,
    value: 0.0
  });
  options.push({
    name: "br-y",
    type: chrome.documentScan.OptionType.FIXED,
    value: 279.4 // 11" in mm
  });
  response = await chrome.documentScan.setOptions(handle, options);
  let imgBlob = await pageAsBlob(handle);
  if (imgBlob != null) {
    // Insert imgBlob into DOM, save to disk, etc
  }
  await chrome.documentScan.closeScanner(handle);
}
```

### Show the configuration

As stated elsewhere, showing a scanner's configuration options to a user requires calling `getOptionGroups()` in addition to the scanner options returned from a call to `openScanner()`. This is so that options can be shown to users in manufacturer-defined groups. This example shows how to do that.

```javascript
async function showConfig() {
  let response = await chrome.documentScan.getScannerList({ secure: true });
  let scanner = await chrome.documentScan.openScanner(
    response.scanners[0].scannerId);
  let groups = await chrome.documentScan.getOptionGroups(scanner.scannerHandle);
  for (const group of groups.groups) {
    console.log("=== " + group.title + " ===");
    for (const member of group.members) {
      const option = scanner.options[member];
      if (option.isActive) {
        console.log("  " + option.name + " = " + option.value);
      } else {
        console.log("  " + option.name + " is inactive");
      }
    }
  }
}
```

## Types

### `CancelScanResponse`

Chrome 125+

#### Properties

*   `job`

    string

    Provides the same job handle that was passed to `cancelScan()`.
*   `result`

    `OperationResult`

    The backend's cancel scan result. If the result is `OperationResult.SUCCESS` or `OperationResult.CANCELLED`, the scan has been cancelled and the scanner is ready to start a new scan. If the result is `OperationResult.DEVICE_BUSY` , the scanner is still processing the requested cancellation; the caller should wait a short time and try the request again. Other result values indicate a permanent error that should not be retried.

### `CloseScannerResponse`

Chrome 125+

#### Properties

*   `result`

    `OperationResult`

    The result of closing the scanner. Even if this value is not `SUCCESS`, the handle will be invalid and should not be used for any further operations.
*   `scannerHandle`

    string

    The same scanner handle as was passed to `closeScanner`.

### `Configurability`

Chrome 125+

How an option can be changed.

#### Enum

*   `"NOT_CONFIGURABLE"`
    The option is read-only.
*   `"SOFTWARE_CONFIGURABLE"`
    The option can be set in software.
*   `"HARDWARE_CONFIGURABLE"`
    The option can be set by the user toggling or pushing a button on the scanner.

### `ConnectionType`

Chrome 125+

Indicates how the scanner is connected to the computer.

#### Enum

*   `"UNSPECIFIED"`
*   `"USB"`
*   `"NETWORK"`

### `ConstraintType`

Chrome 125+

The data type of constraint represented by an `OptionConstraint`.

#### Enum

*   `"INT_RANGE"`
    The constraint on a range of `OptionType.INT` values. The `min`, `max`, and `quant` properties of `OptionConstraint` will be long, and its `list` propety will be unset.
*   `"FIXED_RANGE"`
    The constraint on a range of `OptionType.FIXED` values. The `min`, `max`, and `quant` properties of `OptionConstraint` will be double, and its `list` property will be unset.
*   `"INT_LIST"`
    The constraint on a specific list of `OptionType.INT` values. The `OptionConstraint.list` property will contain long values, and the other properties will be unset.
*   `"FIXED_LIST"`
    The constraint on a specific list of `OptionType.FIXED` values. The `OptionConstraint.list` property will contain double values, and the other properties will be unset.
*   `"STRING_LIST"`
    The constraint on a specific list of `OptionType.STRING` values. The `OptionConstraint.list` property will contain DOMString values, and the other properties will be unset.

### `DeviceFilter`

Chrome 125+

#### Properties

*   `local`

    boolean optional

    Only return scanners that are directly attached to the computer.
*   `secure`

    boolean optional

    Only return scanners that use a secure transport, such as USB or TLS.

### `GetOptionGroupsResponse`

Chrome 125+

#### Properties

*   `groups`

    `OptionGroup[]` optional

    If `result` is `SUCCESS`, provides a list of option groups in the order supplied by the scanner driver.
*   `result`

    `OperationResult`

    The result of getting the option groups. If the value of this is `SUCCESS`, the `groups` property will be populated.
*   `scannerHandle`

    string

    The same scanner handle as was passed to `getOptionGroups`.

### `GetScannerListResponse`

Chrome 125+

#### Properties

*   `result`

    `OperationResult`

    The enumeration result. Note that partial results could be returned even if this indicates an error.
*   `scanners`

    `ScannerInfo[]`

    A possibly-empty list of scanners that match the provided `DeviceFilter`.

### `OpenScannerResponse`

Chrome 125+

#### Properties

*   `options`

    object optional

    If `result` is `SUCCESS`, provides a key-value mapping where the key is a device-specific option and the value is an instance of `ScannerOption`.
*   `result`

    `OperationResult`

    The result of opening the scanner. If the value of this is `SUCCESS`, the `scannerHandle` and `options` properties will be populated.
*   `scannerHandle`

    string optional

    If `result` is `SUCCESS`, a handle to the scanner that can be used for further operations.
*   `scannerId`

    string

    The scanner ID passed to `openScanner()`.

### `OperationResult`

Chrome 125+

An enum that indicates the result of each operation.

#### Enum

*   `"UNKNOWN"`
    An unknown or generic failure occurred.
*   `"SUCCESS"`
    The operation succeeded.
*   `"UNSUPPORTED"`
    The operation is not supported.
*   `"CANCELLED"`
    The operation was cancelled.
*   `"DEVICE_BUSY"`
    The device is busy.
*   `"INVALID"`
    Either the data or an argument passed to the method is not valid.
*   `"WRONG_TYPE"`
    The supplied value is the wrong data type for the underlying option.
*   `"EOF"`
    No more data is available.
*   `"ADF_JAMMED"`
    The document feeder is jammed.
*   `"ADF_EMPTY"`
    The document feeder is empty.
*   `"COVER_OPEN"`
    The flatbed cover is open.
*   `"IO_ERROR"`
    An error occurred while communicating with the device.
*   `"ACCESS_DENIED"`
    The device requires authentication.
*   `"NO_MEMORY"`
    Not enough memory is available on the Chromebook to complete the operation.
*   `"UNREACHABLE"`
    The device is not reachable.
*   `"MISSING"`
    The device is disconnected.
*   `"INTERNAL_ERROR"`
    An error has occurred somewhere other than the calling application.

### `OptionConstraint`

Chrome 125+

#### Properties

*   `list`

    `string[]` | `number[]` optional
*   `max`

    number optional
*   `min`

    number optional
*   `quant`

    number optional
*   `type`

    `ConstraintType`

### `OptionGroup`

Chrome 125+

#### Properties

*   `members`

    `string[]`

    An array of option names in driver-provided order.
*   `title`

    string

    Provides a printable title, for example "Geometry options".

### `OptionSetting`

Chrome 125+

#### Properties

*   `name`

    string

    Indicates the name of the option to set.
*   `type`

    `OptionType`

    Indicates the data type of the option. The requested data type must match the real data type of the underlying option.
*   `value`

    string | number | boolean | `number[]` optional

    Indicates the value to set. Leave unset to request automatic setting for options that have `autoSettable` enabled. The data type supplied for `value` must match `type`.

### `OptionType`

Chrome 125+

The data type of an option.

#### Enum

*   `"UNKNOWN"`
    The option's data type is unknown. The `value` property will be unset.
*   `"BOOL"`
    The `value` property will be one of `true` or `false`.
*   `"INT"`
    A signed 32-bit integer. The `value` property will be `long` or `long[]`, depending on whether the option takes more than one value.
*   `"FIXED"`
    A double in the range -32768-32767.9999 with a resolution of 1/65535. The `value` property will be `double` or `double[]` depending on whether the option takes more than one value. Double values that can't be exactly represented will be rounded to the available range and precision.
*   `"STRING"`
    A sequence of any bytes except NUL ('\0'). The `value` property will be a DOMString.
*   `"BUTTON"`
    An option of this type has no value. Instead, setting an option of this type causes an option-specific side effect in the scanner driver. For example, a button-typed option could be used by a scanner driver to provide a means to select default values or to tell an automatic document feeder to advance to the next sheet of paper.
*   `"GROUP"`
    Grouping option. No value. This is included for compatibility, but will not normally be returned in `ScannerOption` values. Use `getOptionGroups()` to retrieve the list of groups with their member options.

### `OptionUnit`

Chrome 125+

Indicates the data type for `ScannerOption.unit`.

#### Enum

*   `"UNITLESS"`
    The value is a unitless number. For example, it can be a threshold.
*   `"PIXEL"`
    The value is a number of pixels, for example, scan dimensions.
*   `"BIT"`
    The value is the number of bits, for example, color depth.
*   `"MM"`
    The value is measured in millimeters, for example, scan dimensions.
*   `"DPI"`
    The value is measured in dots per inch, for example, resolution.
*   `"PERCENT"`
    The value is a percent.

===

---
title: chrome.dom
url: https://developer.chrome.com/docs/extensions/reference/api/dom
---

## Description

Use the `chrome.dom` API to access special DOM APIs for Extensions

## Availability

Chrome 88+

## Methods

### `openOrClosedShadowRoot()`

```
chrome.dom.openOrClosedShadowRoot( element: HTMLElement, )
```

Gets the open shadow root or the closed shadow root hosted by the specified element. If the element doesn't attach the shadow root, it will return null.

#### Parameters

*   `element`

    `HTMLElement`

#### Returns

*   `object`

    See https://developer.mozilla.org/en-US/docs/Web/API/ShadowRoot

===

---
title: chrome.downloads
url: https://developer.chrome.com/docs/extensions/reference/api/downloads
---

## Description

Use the `chrome.downloads` API to programmatically initiate, monitor, manipulate, and search for downloads.

## Permissions

`downloads`

You must declare the `"downloads"` permission in the extension manifest to use this API.

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "downloads"
  ],
  ...
}
```

## Examples

You can find simple examples of using the `chrome.downloads` API in the `examples/api/downloads` directory. For other examples and for help in viewing the source code, see Samples.

## Types

### `BooleanDelta`

#### Properties

*   `current`

    boolean optional
*   `previous`

    boolean optional

### `DangerType`

*   `file`
    The download's filename is suspicious.
*   `url`
    The download's URL is known to be malicious.
*   `content`
    The downloaded file is known to be malicious.
*   `uncommon`
    The download's URL is not commonly downloaded and could be dangerous.
*   `host`
    The download came from a host known to distribute malicious binaries and is likely dangerous.
*   `unwanted`
    The download is potentially unwanted or unsafe. E.g. it could make changes to browser or computer settings.
*   `safe`
    The download presents no known danger to the user's computer.
*   `accepted`
    The user has accepted the dangerous download.

#### Enum

*   `"file"`
*   `"url"`
*   `"content"`
*   `"uncommon"`
*   `"host"`
*   `"unwanted"`
*   `"safe"`
*   `"accepted"`
*   `"allowlistedByPolicy"`
*   `"asyncScanning"`
*   `"asyncLocalPasswordScanning"`
*   `"passwordProtected"`
*   `"blockedTooLarge"`
*   `"sensitiveContentWarning"`
*   `"sensitiveContentBlock"`
*   `"deepScannedFailed"`
*   `"deepScannedSafe"`
*   `"deepScannedOpenedDangerous"`
*   `"promptForScanning"`
*   `"promptForLocalPasswordScanning"`
*   `"accountCompromise"`
*   `"blockedScanFailed"`

### `DoubleDelta`

#### Properties

*   `current`

    number optional
*   `previous`

    number optional

### `DownloadDelta`

#### Properties

*   `canResume`

    `BooleanDelta` optional

    The change in `canResume`, if any.
*   `danger`

    `StringDelta` optional

    The change in `danger`, if any.
*   `endTime`

    `StringDelta` optional

    The change in `endTime`, if any.
*   `error`

    `StringDelta` optional

    The change in `error`, if any.
*   `exists`

    `BooleanDelta` optional

    The change in `exists`, if any.
*   `fileSize`

    `DoubleDelta` optional

    The change in `fileSize`, if any.
*   `filename`

    `StringDelta` optional

    The change in `filename`, if any.
*   `finalUrl`

    `StringDelta` optional

    Chrome 54+

    The change in `finalUrl`, if any.
*   `id`

    number

    The id of the `DownloadItem` that changed.
*   `mime`

    `StringDelta` optional

    The change in `mime`, if any.
*   `paused`

    `BooleanDelta` optional

    The change in `paused`, if any.
*   `startTime`

    `StringDelta` optional

    The change in `startTime`, if any.
*   `state`

    `StringDelta` optional

    The change in `state`, if any.
*   `totalBytes`

    `DoubleDelta` optional

    The change in `totalBytes`, if any.
*   `url`

    `StringDelta` optional

    The change in `url`, if any.

### `DownloadItem`

#### Properties

*   `byExtensionId`

    string optional

    The identifier for the extension that initiated this download if this download was initiated by an extension. Does not change once it is set.
*   `byExtensionName`

    string optional

    The localized name of the extension that initiated this download if this download was initiated by an extension. May change if the extension changes its name or if the user changes their locale.
*   `bytesReceived`

    number

    Number of bytes received so far from the host, without considering file compression.
*   `canResume`

    boolean

    True if the download is in progress and paused, or else if it is interrupted and can be resumed starting from where it was interrupted.
*   `danger`

    `DangerType`

    Indication of whether this download is thought to be safe or known to be suspicious.
*   `endTime`

    string optional

    The time when the download ended in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){if (item.endTime) console.log(new Date(item.endTime))})})`
*   `error`

    `InterruptReason` optional

    Why the download was interrupted. Several kinds of HTTP errors may be grouped under one of the errors beginning with `SERVER_`. Errors relating to the network begin with `NETWORK_`, errors relating to the process of writing the file to the file system begin with `FILE_`, and interruptions initiated by the user begin with `USER_`.
*   `estimatedEndTime`

    string optional

    Estimated time when the download will complete in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){if (item.estimatedEndTime) console.log(new Date(item.estimatedEndTime))})})`
*   `exists`

    boolean

    Whether the downloaded file still exists. This information may be out of date because Chrome does not automatically watch for file removal. Call `search()` in order to trigger the check for file existence. When the existence check completes, if the file has been deleted, then an `onChanged` event will fire. Note that `search()` does not wait for the existence check to finish before returning, so results from `search()` may not accurately reflect the file system. Also, `search()` may be called as often as necessary, but will not check for file existence any more frequently than once every 10 seconds.
*   `fileSize`

    number

    Number of bytes in the whole file post-decompression, or -1 if unknown.
*   `filename`

    string

    Absolute local path.
*   `finalUrl`

    string

    Chrome 54+

    The absolute URL that this download is being made from, after all redirects.
*   `id`

    number

    An identifier that is persistent across browser sessions.
*   `incognito`

    boolean

    False if this download is recorded in the history, true if it is not recorded.
*   `mime`

    string

    The file's MIME type.
*   `paused`

    boolean

    True if the download has stopped reading data from the host, but kept the connection open.
*   `referrer`

    string

    Absolute URL.
*   `startTime`

    string

    The time when the download began in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){console.log(new Date(item.startTime))})})`
*   `state`

    `State`

    Indicates whether the download is progressing, interrupted, or complete.
*   `totalBytes`

    number

    Number of bytes in the whole file, without considering file compression, or -1 if unknown.
*   `url`

    string

    The absolute URL that this download initiated from, before any redirects.

### `DownloadOptions`

#### Properties

*   `body`

    string optional

    Post body.
*   `conflictAction`

    `FilenameConflictAction` optional

    The action to take if `filename` already exists.
*   `filename`

    string optional

    A file path relative to the Downloads directory to contain the downloaded file, possibly containing subdirectories. Absolute paths, empty paths, and paths containing back-references `".."` will cause an error. `onDeterminingFilename` allows suggesting a filename after the file's MIME type and a tentative filename have been determined.
*   `headers`

    `HeaderNameValuePair[]` optional

    Extra HTTP headers to send with the request if the URL uses the HTTP[s] protocol. Each header is represented as a dictionary containing the keys `name` and either `value` or `binaryValue`, restricted to those allowed by `XMLHttpRequest`.
*   `method`

    `HttpMethod` optional

    The HTTP method to use if the URL uses the HTTP[S] protocol.
*   `saveAs`

    boolean optional

    Use a file-chooser to allow the user to select a filename regardless of whether `filename` is set or already exists.
*   `url`

    string

    The URL to download.

### `DownloadQuery`

#### Properties

*   `bytesReceived`

    number optional

    Number of bytes received so far from the host, without considering file compression.
*   `danger`

    `DangerType` optional

    Indication of whether this download is thought to be safe or known to be suspicious.
*   `endTime`

    string optional

    The time when the download ended in ISO 8601 format.
*   `endedAfter`

    string optional

    Limits results to `DownloadItem` that ended after the given ms in ISO 8601 format
*   `endedBefore`

    string optional

    Limits results to `DownloadItem` that ended before the given ms in ISO 8601 format.
*   `error`

    `InterruptReason` optional

    Why a download was interrupted.
*   `exists`

    boolean optional

    Whether the downloaded file exists;
*   `fileSize`

    number optional

    Number of bytes in the whole file post-decompression, or -1 if unknown.
*   `filename`

    string optional

    Absolute local path.
*   `filenameRegex`

    string optional

    Limits results to `DownloadItem` whose `filename` matches the given regular expression.
*   `finalUrl`

    string optional

    Chrome 54+

    The absolute URL that this download is being made from, after all redirects.
*   `finalUrlRegex`

    string optional

    Chrome 54+

    Limits results to `DownloadItem` whose `finalUrl` matches the given regular expression.
*   `id`

    number optional

    The `id` of the `DownloadItem` to query.
*   `limit`

    number optional

    The maximum number of matching `DownloadItem` returned. Defaults to 1000. Set to 0 in order to return all matching `DownloadItem`. See `search` for how to page through results.
*   `mime`

    string optional

    The file's MIME type.
*   `orderBy`

    `string[]` optional

    Set elements of this array to `DownloadItem` properties in order to sort search results. For example, setting `orderBy=['startTime']` sorts the `DownloadItem` by their start time in ascending order. To specify descending order, prefix with a hyphen: `'-startTime'`.
*   `paused`

    boolean optional

    True if the download has stopped reading data from the host, but kept the connection open.
*   `query`

    `string[]` optional

    This array of search terms limits results to `DownloadItem` whose `filename` or `url` or `finalUrl` contain all of the search terms that do not begin with a dash `'-'` and none of the search terms that do begin with a dash.
*   `startTime`

    string optional

    The time when the download began in ISO 8601 format.
*   `startedAfter`

    string optional

    Limits results to `DownloadItem` that started after the given ms in ISO 8601 format.
*   `startedBefore`

    string optional

    Limits results to `DownloadItem` that started before the given ms in ISO 8601 format.
*   `state`

    `State` optional

    Indicates whether the download is progressing, interrupted, or complete.
*   `totalBytes`

    number optional

    Number of bytes in the whole file, without considering file compression, or -1 if unknown.
*   `totalBytesGreater`

    number optional

    Limits results to `DownloadItem` whose `totalBytes` is greater than the given integer.
*   `totalBytesLess`

    number optional

    Limits results to `DownloadItem` whose `totalBytes` is less than the given integer.
*   `url`

    string optional

    The absolute URL that this download initiated from, before any redirects.
*   `urlRegex`

    string optional

    Limits results to `DownloadItem` whose `url` matches the given regular expression.

### `FilenameConflictAction`

*   `uniquify`
    To avoid duplication, the filename is changed to include a counter before the filename extension.
*   `overwrite`
    The existing file will be overwritten with the new file.
*   `prompt`
    The user will be prompted with a file chooser dialog.

#### Enum

*   `"uniquify"`
*   `"overwrite"`
*   `"prompt"`

### `FilenameSuggestion`

#### Properties

*   `conflictAction`

    `FilenameConflictAction` optional

    The action to take if `filename` already exists.
*   `filename`

    string

    The `DownloadItem`'s new target `DownloadItem.filename`, as a path relative to the user's default Downloads directory, possibly containing subdirectories. Absolute paths, empty paths, and paths containing back-references `".."` will be ignored. `filename` is ignored if there are any `onDeterminingFilename` listeners registered by any extensions.

### `GetFileIconOptions`

#### Properties

*   `size`

    number optional

    The size of the returned icon. The icon will be square with dimensions `size` \* `size` pixels. The default and largest size for the icon is 32x32 pixels. The only supported sizes are 16 and 32. It is an error to specify any other size.

### `HeaderNameValuePair`

#### Properties

*   `name`

    string

    Name of the HTTP header.
*   `value`

    string

    Value of the HTTP header.

### `HttpMethod`

#### Enum

*   `"GET"`
*   `"POST"`

### `InterruptReason`

#### Enum

*   `"FILE_FAILED"`
*   `"FILE_ACCESS_DENIED"`
*   `"FILE_NO_SPACE"`
*   `"FILE_NAME_TOO_LONG"`
*   `"FILE_TOO_LARGE"`
*   `"FILE_VIRUS_INFECTED"`
*   `"FILE_TRANSIENT_ERROR"`
*   `"FILE_BLOCKED"`
*   `"FILE_SECURITY_CHECK_FAILED"`
*   `"FILE_TOO_SHORT"`
*   `"FILE_HASH_MISMATCH"`
*   `"FILE_SAME_AS_SOURCE"`
*   `"NETWORK_FAILED"`
*   `"NETWORK_TIMEOUT"`
*   `"NETWORK_DISCONNECTED"`
*   `"NETWORK_SERVER_DOWN"`
*   `"NETWORK_INVALID_REQUEST"`
*   `"SERVER_FAILED"`
*   `"SERVER_NO_RANGE"`
*   `"SERVER_BAD_CONTENT"`
*   `"SERVER_UNAUTHORIZED"`
*   `"SERVER_CERT_PROBLEM"`
*   `"SERVER_FORBIDDEN"`
*   `"SERVER_UNREACHABLE"`
*   `"SERVER_CONTENT_LENGTH_MISMATCH"`
*   `"SERVER_CROSS_ORIGIN_REDIRECT"`
*   `"USER_CANCELED"`
*   `"USER_SHUTDOWN"`
*   `"CRASH"`

### `State`

*   `in_progress`
    The download is currently receiving data from the server.
*   `interrupted`
    An error broke the connection with the file host.
*   `complete`
    The download completed successfully.

#### Enum

*   `"in_progress"`
*   `"interrupted"`
*   `"complete"`

### `StringDelta`

#### Properties

*   `current`

    string optional
*   `previous`

    string optional

### `UiOptions`

Chrome 105+

#### Properties

*   `enabled`

    boolean

    Enable or disable the download UI.

## Methods

### `acceptDanger()`

Promise

```
chrome.downloads.acceptDanger( downloadId: number, callback?: function, )
```

Prompt the user to accept a dangerous download. Can only be called from a visible context (tab, window, or page/browser action popup). Does not automatically accept dangerous downloads. If the download is accepted, then an `onChanged` event will fire, otherwise nothing will happen. When all the data is fetched into a temporary file and either the download is not dangerous or the danger has been accepted, then the temporary file is renamed to the target filename, the state changes to `'complete'`, and `onChanged` fires.

#### Parameters

*   `downloadId`

    number

    The identifier for the `DownloadItem`.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `cancel()`

Promise

```
chrome.downloads.cancel( downloadId: number, callback?: function, )
```

Cancel a download. When `callback` is run, the download is cancelled, completed, interrupted or doesn't exist anymore.

#### Parameters

*   `downloadId`

    number

    The `id` of the download to cancel.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `download()`

Promise

```
chrome.downloads.download( options: DownloadOptions, callback?: function, )
```

Download a URL. If the URL uses the HTTP[S] protocol, then the request will include all cookies currently set for its hostname. If both `filename` and `saveAs` are specified, then the Save As dialog will be displayed, pre-populated with the specified `filename`. If the download started successfully, `callback` will be called with the new `DownloadItem`'s `downloadId`. If there was an error starting the download, then `callback` will be called with `downloadId=undefined` and `runtime.lastError` will contain a descriptive string. The error strings are not guaranteed to remain backwards compatible between releases. Extensions must not parse it.

#### Parameters

*   `options`

    `DownloadOptions`

    What to download and how.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (downloadId: number) => void
    ```

    *   `downloadId`

        number

#### Returns

*   `Promise<number>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `erase()`

Promise

```
chrome.downloads.erase( query: DownloadQuery, callback?: function, )
```

Erase matching `DownloadItem` from history without deleting the downloaded file. An `onErased` event will fire for each `DownloadItem` that matches `query`, then `callback` will be called.

#### Parameters

*   `query`

    `DownloadQuery`
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (erasedIds: number[]) => void
    ```

    *   `erasedIds`

        `number[]`

#### Returns

*   `Promise<number[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getFileIcon()`

Promise

```
chrome.downloads.getFileIcon( downloadId: number, options?: GetFileIconOptions, callback?: function, )
```

Retrieve an icon for the specified download. For new downloads, file icons are available after the `onCreated` event has been received. The image returned by this function while a download is in progress may be different from the image returned after the download is complete. Icon retrieval is done by querying the underlying operating system or toolkit depending on the platform. The icon that is returned will therefore depend on a number of factors including state of the download, platform, registered file types and visual theme. If a file icon cannot be determined, `runtime.lastError` will contain an error message.

#### Parameters

*   `downloadId`

    number

    The identifier for the download.
*   `options`

    `GetFileIconOptions` optional
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (iconURL?: string) => void
    ```

    *   `iconURL`

        string optional

#### Returns

*   `Promise<string | undefined>`

    Chrome 96+

===

---
title: chrome.enterprise.deviceAttributes
url: https://developer.chrome.com/docs/extensions/reference/api/enterprise/deviceAttributes
---
# chrome.enterprise.deviceAttributes

This API is only for extensions installed by a policy.Important: This API works only on ChromeOS.

## Description

Use the `chrome.enterprise.deviceAttributes` API to read device attributes. Note: This API is only available to extensions force-installed by enterprise policy.

## Permissions

`enterprise.deviceAttributes`

## Availability

Chrome 46+ ChromeOS only Requires policy

## Methods

### getDeviceAnnotatedLocation()

Promise Chrome 66+

```
chrome.enterprise.deviceAttributes.getDeviceAnnotatedLocation( callback?: function, )
```

Fetches the administrator-annotated Location. If the current user is not affiliated or no Annotated Location has been set by the administrator, returns an empty `string`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (annotatedLocation: string) => void
  ```

  + `annotatedLocation`

    `string`

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getDeviceAssetId()

Promise Chrome 66+

```
chrome.enterprise.deviceAttributes.getDeviceAssetId( callback?: function, )
```

Fetches the administrator-annotated Asset Id. If the current user is not affiliated or no Asset Id has been set by the administrator, returns an empty `string`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (assetId: string) => void
  ```

  + `assetId`

    `string`

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getDeviceHostname()

Promise Chrome 82+

```
chrome.enterprise.deviceAttributes.getDeviceHostname( callback?: function, )
```

Fetches the device's `hostname` as set by `DeviceHostnameTemplate` policy. If the current user is not affiliated or no `hostname` has been set by the enterprise policy, returns an empty `string`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (hostname: string) => void
  ```

  + `hostname`

    `string`

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getDeviceSerialNumber()

Promise Chrome 66+

```
chrome.enterprise.deviceAttributes.getDeviceSerialNumber( callback?: function, )
```

Fetches the device's `serialNumber`. Please note the purpose of this API is to administrate the device (e.g. generating Certificate Sign Requests for device-wide certificates). This API may not be used for tracking devices without the consent of the device's administrator. If the current user is not affiliated, returns an empty `string`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (serialNumber: string) => void
  ```

  + `serialNumber`

    `string`

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getDirectoryDeviceId()

Promise

```
chrome.enterprise.deviceAttributes.getDirectoryDeviceId( callback?: function, )
```

Fetches the value of the device identifier of the directory API, that is generated by the server and identifies the cloud record of the device for querying in the cloud directory API. If the current user is not affiliated, returns an empty `string`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (deviceId: string) => void
  ```

  + `deviceId`

    `string`

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

===

---
title: chrome.enterprise.hardwarePlatform
url: https://developer.chrome.com/docs/extensions/reference/api/enterprise/hardwarePlatform
---
# chrome.enterprise.hardwarePlatform

This API is only for extensions installed by a policy. The `EnterpriseHardwarePlatformAPIEnabled` key must also be set.

## Description

Use the `chrome.enterprise.hardwarePlatform` API to get the manufacturer and model of the hardware platform where the browser runs. Note: This API is only available to extensions installed by enterprise policy.

## Permissions

`enterprise.hardwarePlatform`

## Availability

Chrome 71+ Requires policy

## Types

### HardwarePlatformInfo

#### Properties

* `manufacturer`

  `string`
* `model`

  `string`

## Methods

### getHardwarePlatformInfo()

Promise

```
chrome.enterprise.hardwarePlatform.getHardwarePlatformInfo( callback?: function, )
```

Obtains the `manufacturer` and `model` for the hardware platform and, if the extension is authorized, returns it via `callback`.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (info: HardwarePlatformInfo) => void
  ```

  + `info`

    `HardwarePlatformInfo`

#### Returns

* `Promise<HardwarePlatformInfo>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

===

---
title: chrome.enterprise.networkingAttributes
url: https://developer.chrome.com/docs/extensions/reference/api/enterprise/networkingAttributes
---
# chrome.enterprise.networkingAttributes

This API is only for extensions installed by a policy.Important: This API works only on ChromeOS.

## Description

Use the `chrome.enterprise.networkingAttributes` API to read information about your current network. Note: This API is only available to extensions force-installed by enterprise policy.

## Permissions

`enterprise.networkingAttributes`

## Availability

Chrome 85+ ChromeOS only Requires policy

## Types

### NetworkDetails

#### Properties

* `ipv4`

  `string` optional

  The device's local IPv4 address (undefined if not configured).
* `ipv6`

  `string` optional

  The device's local IPv6 address (undefined if not configured).
* `macAddress`

  `string`

  The device's MAC address.

## Methods

### getNetworkDetails()

Promise

```
chrome.enterprise.networkingAttributes.getNetworkDetails( callback?: function, )
```

Retrieves the network details of the device's default network. If the user is not affiliated or the device is not connected to a network, `runtime.lastError` will be set with a failure reason.

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (networkAddresses: NetworkDetails) => void
  ```

  + `networkAddresses`

    `NetworkDetails`

#### Returns

* `Promise<NetworkDetails>`

  Chrome 96+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

===

---
title: chrome.enterprise.platformKeys
url: https://developer.chrome.com/docs/extensions/reference/api/enterprise/platformKeys
---
# chrome.enterprise.platformKeys

This API is only for extensions installed by a policy.Important: This API works only on ChromeOS.

## Description

Use the `chrome.enterprise.platformKeys` API to generate keys and install certificates for these keys. The certificates will be managed by the platform and can be used for TLS authentication, network access or by other extension through `chrome.platformKeys`.

## Permissions

`enterprise.platformKeys`

## Availability

ChromeOS only Requires policy

## Concepts and usage

Typical usage of this API to enroll a client certificate follows these steps:

* Get all available tokens using `enterprise.platformKeys.getTokens()`.
* Find the `Token` with `id` equal to `"user"`. Use this `Token` subsequently.
* Generate a key pair using the `generateKey()` `Token` method (defined in `SubtleCrypto`). This will return handle to the key.
* Export the public key using the `exportKey()` `Token` method (defined in `SubtleCrypto`).
* Create the signature of the certification request's data using the `sign()` `Token` method (defined in `SubtleCrypto`).
* Complete the certification request and send it to the certification authority.
* If a certificate is received, import it using `enterprise.platformKeys.importCertificate()`

Here's an example that shows the major API interaction except the building and sending of the certification request:

```javascript
function getUserToken(callback) { chrome.enterprise.platformKeys.getTokens(function(tokens) { for (var i = 0; i < tokens.length; i++) { if (tokens[i].id == "user") { callback(tokens[i]); return; } } callback(undefined); }); }
function generateAndSign(userToken) {
  var data = new Uint8Array([0, 5, 1, 2, 3, 4, 5, 6]);
  var algorithm = {
    name: "RSASSA-PKCS1-v1_5",
    // RsaHashedKeyGenParams
    modulusLength: 2048,
    publicExponent: new Uint8Array([0x01, 0x00, 0x01]), // Equivalent to 65537
    hash: {
      name: "SHA-256",
    }
  };
  var cachedKeyPair;
  userToken.subtleCrypto.generateKey(algorithm, false, ["sign"])
    .then(function(keyPair) {
      cachedKeyPair = keyPair;
      return userToken.subtleCrypto.exportKey("spki", keyPair.publicKey);
    }, console.log.bind(console))
    .then(function(publicKeySpki) {
      // Build the Certification Request using the public key.
      return userToken.subtleCrypto.sign(
        {name : "RSASSA-PKCS1-v1_5"},
        cachedKeyPair.privateKey,
        data);
    }, console.log.bind(console))
    .then(function(signature) {
      // Complete the Certification Request with |signature|.
      // Send out the request to the CA, calling back
      // onClientCertificateReceived.
    }, console.log.bind(console));
}
function onClientCertificateReceived(userToken, certificate) {
  chrome.enterprise.platformKeys.importCertificate(userToken.id, certificate);
}
getUserToken(generateAndSign);
```

## Types

### Algorithm

Chrome 110+

Type of key to generate.

#### Enum

"RSA"

"ECDSA"

### ChallengeKeyOptions

Chrome 110+

#### Properties

* `challenge`

  `ArrayBuffer`

  A challenge as emitted by the Verified Access Web API.
* `registerKey`

  `RegisterKeyOptions` optional

  If present, registers the challenged key with the specified scope's token. The key can then be associated with a certificate and used like any other signing key. Subsequent calls to this `function` will then generate a new Enterprise Key in the specified scope.
* `scope`

  `Scope`

  Which Enterprise Key to challenge.

### RegisterKeyOptions

Chrome 110+

#### Properties

* `algorithm`

  `Algorithm`

  Which algorithm the registered key should use.

### Scope

Chrome 110+

Whether to use the Enterprise User Key or the Enterprise Machine Key.

#### Enum

"USER"

"MACHINE"

### Token

#### Properties

* `id`

  `string`

  Uniquely identifies this `Token`.

  Static IDs are `"user"` and `"system"`, referring to the platform's user-specific and the system-wide hardware token, respectively. Any other tokens (with other identifiers) might be returned by `enterprise.platformKeys.getTokens`.
* `softwareBackedSubtleCrypto`

  `SubtleCrypto`

  Chrome 97+

  Implements the WebCrypto's `SubtleCrypto` interface. The cryptographic operations, including key generation, are software-backed. Protection of the keys, and thus implementation of the non-extractable property, is done in software, so the keys are less protected than hardware-backed keys.

  Only non-extractable keys can be generated. The supported key types are `RSASSA-PKCS1-V1_5` and `RSA-OAEP` (on Chrome versions 135+) with `modulusLength` up to 2048. Each `RSASSA-PKCS1-V1_5` key can be used for signing data at most once, unless the extension is allowlisted through the `KeyPermissions` policy, in which case the key can be used indefinitely. `RSA-OAEP` keys are supported since Chrome version 135 and can be used by extensions allowlisted through that same policy to unwrap other keys.

  Keys generated on a specific `Token` cannot be used with any other Tokens, nor can they be used with `window.crypto.subtle`. Equally, `Key` objects created with `window.crypto.subtle` cannot be used with this interface.
* `subtleCrypto`

  `SubtleCrypto`

  Implements the WebCrypto's `SubtleCrypto` interface. The cryptographic operations, including key generation, are hardware-backed.

  Only non-extractable keys can be generated. The supported key types are `RSASSA-PKCS1-V1_5` and `RSA-OAEP` (on Chrome versions 135+) with `modulusLength` up to 2048 and `ECDSA` with `namedCurve` P-256. Each `RSASSA-PKCS1-V1_5` and `ECDSA` key can be used for signing data at most once, unless the extension is allowlisted through the `KeyPermissions` policy, in which case the key can be used indefinitely. `RSA-OAEP` keys are supported since Chrome version 135 and can be used by extensions allowlisted through that same policy to unwrap other keys.

  Keys generated on a specific `Token` cannot be used with any other Tokens, nor can they be used with `window.crypto.subtle`. Equally, `Key` objects created with `window.crypto.subtle` cannot be used with this interface.

## Methods

### challengeKey()

Promise Chrome 110+

```
chrome.enterprise.platformKeys.challengeKey( options: ChallengeKeyOptions, callback?: function, )
```

Similar to `challengeMachineKey` and `challengeUserKey`, but allows specifying the algorithm of a registered key. Challenges a hardware-backed Enterprise Machine Key and emits the response as part of a remote attestation protocol. Only useful on ChromeOS and in conjunction with the Verified Access Web API which both issues challenges and verifies responses.

A successful verification by the Verified Access Web API is a strong signal that the current device is a legitimate ChromeOS device, the current device is managed by the domain specified during verification, the current signed-in user is managed by the domain specified during verification, and the current device state complies with enterprise device policy. For example, a policy may specify that the device must not be in developer mode. Any device identity emitted by the verification is tightly bound to the hardware of the current device. If `"user"` `Scope` is specified, the identity is also tightly bound to the current signed-in user.

This `function` is highly restricted and will fail if the current device is not managed, the current user is not managed, or if this operation has not explicitly been enabled for the caller by enterprise device policy. The challenged key does not reside in the `"system"` or `"user"` token and is not accessible by any other API.

#### Parameters

* `options`

  `ChallengeKeyOptions`

  Object containing the fields defined in `ChallengeKeyOptions`.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (response: ArrayBuffer) => void
  ```

  + `response`

    `ArrayBuffer`

    The challenge response.

#### Returns

* `Promise<ArrayBuffer>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### challengeMachineKey()

Promise Chrome 50+ Deprecated since Chrome 110

```
chrome.enterprise.platformKeys.challengeMachineKey( challenge: ArrayBuffer, registerKey?: boolean, callback?: function, )
```

Use `challengeKey` instead.

Challenges a hardware-backed Enterprise Machine Key and emits the response as part of a remote attestation protocol. Only useful on ChromeOS and in conjunction with the Verified Access Web API which both issues challenges and verifies responses. A successful verification by the Verified Access Web API is a strong signal of all of the following: \* The current device is a legitimate ChromeOS device. \* The current device is managed by the domain specified during verification. \* The current signed-in user is managed by the domain specified during verification. \* The current device state complies with enterprise device policy. For example, a policy may specify that the device must not be in developer mode. \* Any device identity emitted by the verification is tightly bound to the hardware of the current device. This `function` is highly restricted and will fail if the current device is not managed, the current user is not managed, or if this operation has not explicitly been enabled for the caller by enterprise device policy. The Enterprise Machine Key does not reside in the `"system"` token and is not accessible by any other API.

#### Parameters

* `challenge`

  `ArrayBuffer`

  A challenge as emitted by the Verified Access Web API.
* `registerKey`

  `boolean` optional

  Chrome 59+

  If set, the current Enterprise Machine Key is registered with the `"system"` token and relinquishes the Enterprise Machine Key role. The key can then be associated with a certificate and used like any other signing key. This key is 2048-bit RSA. Subsequent calls to this `function` will then generate a new Enterprise Machine Key.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (response: ArrayBuffer) => void
  ```

  + `response`

    `ArrayBuffer`

    The challenge response.

#### Returns

* `Promise<ArrayBuffer>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### challengeUserKey()

Promise Chrome 50+ Deprecated since Chrome 110

```
chrome.enterprise.platformKeys.challengeUserKey( challenge: ArrayBuffer, registerKey: boolean, callback?: function, )
```

Use `challengeKey` instead.

Challenges a hardware-backed Enterprise User Key and emits the response as part of a remote attestation protocol. Only useful on ChromeOS and in conjunction with the Verified Access Web API which both issues challenges and verifies responses. A successful verification by the Verified Access Web API is a strong signal of all of the following: \* The current device is a legitimate ChromeOS device. \* The current device is managed by the domain specified during verification. \* The current signed-in user is managed by the domain specified during verification. \* The current device state complies with enterprise user policy. For example, a policy may specify that the device must not be in developer mode. \* The public key emitted by the verification is tightly bound to the hardware of the current device and to the current signed-in user. This `function` is highly restricted and will fail if the current device is not managed, the current user is not managed, or if this operation has not explicitly been enabled for the caller by enterprise user policy. The Enterprise User Key does not reside in the `"user"` token and is not accessible by any other API.

#### Parameters

* `challenge`

  `ArrayBuffer`

  A challenge as emitted by the Verified Access Web API.
* `registerKey`

  `boolean`

  If set, the current Enterprise User Key is registered with the `"user"` token and relinquishes the Enterprise User Key role. The key can then be associated with a certificate and used like any other signing key. This key is 2048-bit RSA. Subsequent calls to this `function` will then generate a new Enterprise User Key.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (response: ArrayBuffer) => void
  ```

  + `response`

    `ArrayBuffer`

    The challenge response.

#### Returns

* `Promise<ArrayBuffer>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getCertificates()

Promise

```
chrome.enterprise.platformKeys.getCertificates( tokenId: string, callback?: function, )
```

Returns the list of all client certificates available from the given token. Can be used to check for the existence and expiration of client certificates that are usable for a certain authentication.

#### Parameters

* `tokenId`

  `string`

  The `id` of a `Token` returned by `getTokens`.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (certificates: ArrayBuffer[]) => void
  ```

  + `certificates`

    `ArrayBuffer[]`

    The list of certificates, each in DER encoding of a X.509 certificate.

#### Returns

* `Promise<ArrayBuffer[]>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### getTokens()

Promise

```
chrome.enterprise.platformKeys.getTokens( callback?: function, )
```

Returns the available Tokens. In a regular user's session the list will always contain the user's token with `id` `"user"`. If a system-wide TPM token is available, the returned list will also contain the system-wide token with `id` `"system"`. The system-wide token will be the same for all sessions on this device (device in the sense of e.g. a Chromebook).

#### Parameters

* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  (tokens: Token[]) => void
  ```

  + `tokens`

    `Token[]`

    The list of available tokens.

#### Returns

* `Promise<Token[]>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### importCertificate()

Promise

```
chrome.enterprise.platformKeys.importCertificate( tokenId: string, certificate: ArrayBuffer, callback?: function, )
```

Imports certificate to the given token if the certified key is already stored in this token. After a successful certification request, this `function` should be used to store the obtained certificate and to make it available to the operating system and browser for authentication.

#### Parameters

* `tokenId`

  `string`

  The `id` of a `Token` returned by `getTokens`.
* `certificate`

  `ArrayBuffer`

  The DER encoding of a X.509 certificate.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

### removeCertificate()

Promise

```
chrome.enterprise.platformKeys.removeCertificate( tokenId: string, certificate: ArrayBuffer, callback?: function, )
```

Removes certificate from the given token if present. Should be used to remove obsolete certificates so that they are not considered during authentication and do not clutter the certificate choice. Should be used to free storage in the certificate store.

#### Parameters

* `tokenId`

  `string`

  The `id` of a `Token` returned by `getTokens`.
* `certificate`

  `ArrayBuffer`

  The DER encoding of a X.509 certificate.
* `callback`

  `function` optional

  The `callback` parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 131+

  Promises are supported in `Manifest V3` and later, but callbacks are provided for backward compatibility. You cannot use both on the same `function` call. The promise resolves with the same type that is passed to the `callback`.

===

---
title: chrome.events
url: https://developer.chrome.com/docs/extensions/reference/api/events
---
# chrome.events

## Description

The `chrome.events` namespace contains common types used by APIs dispatching events to notify you when something interesting happens.

## Concepts and usage

An `Event` is an object that lets you be notified when something interesting happens. Here's an example of using the `chrome.alarms.onAlarm` event to be notified whenever an alarm has elapsed:

```javascript
chrome.alarms.onAlarm.addListener((alarm) => {
  appendToLog(`alarms.onAlarm -- name: ${alarm.name}, scheduledTime: ${alarm.scheduledTime}`);
});
```

As the example shows, you register for notification using `addListener()`. The argument to `addListener()` is always a `function` that you define to handle the event, but the parameters to the `function` depend on which event you're handling. Checking the documentation for `alarms.onAlarm`, you can see that the `function` has a single parameter: an `alarms.Alarm` object that has details about the elapsed alarm.

Example APIs using Events: `alarms`, `i18n`, `identity`, `runtime`. Most `chrome` APIs do.

### Declarative Event Handlers

The declarative event handlers provide a means to define rules consisting of declarative conditions and actions. Conditions are evaluated in the browser rather than the JavaScript engine which reduces roundtrip latencies and allows for very high efficiency.

Declarative event handlers are used for example in the Declarative Content API. This page describes the underlying concepts of all declarative event handlers.

#### Rules

The simplest possible rule consists of one or more conditions and one or more actions:

```javascript
const rule = {
  conditions: [ /* my conditions */ ],
  actions: [ /* my actions */ ]
};
```

If any of the conditions is fulfilled, all actions are executed.

In addition to conditions and actions you may give each rule an `identifier`, which simplifies unregistering previously registered rules, and a `priority` to define precedences among rules. Priorities are only considered if rules conflict each other or need to be executed in a specific order. Actions are executed in descending order of the `priority` of their rules.

```javascript
const rule = {
  id: "my rule", // optional, will be generated if not set.
  priority: 100, // optional, defaults to 100.
  conditions: [ /* my conditions */ ],
  actions: [ /* my actions */ ]
};
```

#### Event objects

Event objects may support rules. These event objects don't call a `callback` `function` when events happen but test whether any registered rule has at least one fulfilled condition and execute the actions associated with this rule. Event objects supporting the declarative API have three relevant methods: `events.Event.addRules()`, `events.Event.removeRules()`, and `events.Event.getRules()`.

#### Add rules

To add rules call the `addRules()` `function` of the event object. It takes an array of rule instances as its first parameter and a `callback` `function` that is called on completion.

```javascript
const rule_list = [rule1, rule2, ...];
addRules(rule_list, (details) => {...});
```

If the rules were inserted successfully, the `details` parameter contains an array of inserted rules appearing in the same order as in the passed `rule_list` where the optional parameters `id` and `priority` were filled with the generated values. If any rule is invalid, for example, because it contained an invalid condition or action, none of the rules are added and the `runtime.lastError` variable is set when the `callback` `function` is called. Each rule in `rule_list` must contain a unique `identifier` that is not already used by another rule or an empty `identifier`.

Note: Rules are persistent across browsing sessions. Therefore, you should install rules during extension installation time using the `runtime.onInstalled` event. Note that this event is also triggered when an extension is updated. Therefore, you should first clear previously installed rules and then register new rules.

#### Remove rules

To remove rules call the `removeRules()` `function`. It accepts an optional array of rule identifiers as its first parameter and a `callback` `function` as its second parameter.

```javascript
const rule_ids = ["id1", "id2", ...];
removeRules(rule_ids, () => {...});
```

If `rule_ids` is an array of identifiers, all rules having identifiers listed in the array are removed. If `rule_ids` lists an `identifier`, that is unknown, this `identifier` is silently ignored. If `rule_ids` is `undefined`, all registered rules of this extension are removed. The `callback()` `function` is called when the rules were removed.

#### Retrieve rules

To retrieve a list of registered rules, call the `getRules()` `function`. It accepts an optional array of rule identifiers with the same semantics as `removeRules()` and a `callback` `function`.

```javascript
const rule_ids = ["id1", "id2", ...];
getRules(rule_ids, (details) => {...});
```

The `details` parameter passed to the `callback()` `function` refers to an array of rules including filled optional parameters.

#### Performance

To achieve maximum performance, you should keep the following guidelines in mind.

Register and unregister rules in bulk. After each registration or unregistration, Chrome needs to update internal data structures. This update is an expensive operation.

Instead of

```javascript
const rule1 = {...};
const rule2 = {...};
chrome.declarativeWebRequest.onRequest.addRules([rule1]);
chrome.declarativeWebRequest.onRequest.addRules([rule2]);
```

Prefer

```javascript
const rule1 = {...};
const rule2 = {...};
chrome.declarativeWebRequest.onRequest.addRules([rule1, rule2]);
```

Prefer substring matching over regular expressions in an `events.UrlFilter`. Substring based matching is extremely fast.

Instead of

```javascript
const match = new chrome.declarativeWebRequest.RequestMatcher({
  url: {urlMatches: "example.com/[^?]*foo" }
});
```

Prefer

```javascript
const match = new chrome.declarativeWebRequest.RequestMatcher({
  url: {hostSuffix: "example.com", pathContains: "foo"}
});
```

If there are many rules that share the same actions, merge the rules into one. Rules trigger their actions as soon as a single condition is fulfilled. This speeds up the matching and reduces memory consumption for duplicate action sets.

Instead of

```javascript
const condition1 = new chrome.declarativeWebRequest.RequestMatcher({ url: { hostSuffix: 'example.com' } });
const condition2 = new chrome.declarativeWebRequest.RequestMatcher({ url: { hostSuffix: 'foobar.com' } });
const rule1 = {
  conditions: [condition1],
  actions: [new chrome.declarativeWebRequest.CancelRequest()]
};
const rule2 = {
  conditions: [condition2],
  actions: [new chrome.declarativeWebRequest.CancelRequest()]
};
chrome.declarativeWebRequest.onRequest.addRules([rule1, rule2]);
```

Prefer

```javascript
const condition1 = new chrome.declarativeWebRequest.RequestMatcher({ url: { hostSuffix: 'example.com' } });
const condition2 = new chrome.declarativeWebRequest.RequestMatcher({ url: { hostSuffix: 'foobar.com' } });
const rule = {
  conditions: [condition1, condition2],
  actions: [new chrome.declarativeWebRequest.CancelRequest()]
};
chrome.declarativeWebRequest.onRequest.addRules([rule]);
```

### Filtered events

Filtered events are a mechanism that allows listeners to specify a subset of events that they are interested in. A listener that uses a filter won't be invoked for events that don't pass the filter, which makes the listening code more declarative and efficient. A service worker need not be woken up to handle events it doesn't care about.

Filtered events are intended to allow a transition from manual filtering code.

Instead of

```javascript
chrome.webNavigation.onCommitted.addListener((event) => {
  if (hasHostSuffix(event.url, 'google.com') || hasHostSuffix(event.url, 'google.com.au')) {
    // ...
  }
});
```

Prefer

```javascript
chrome.webNavigation.onCommitted.addListener((event) => {
  // ...
}, {url: [{hostSuffix: 'google.com'}, {hostSuffix: 'google.com.au'}]});
```

Events support specific filters that are meaningful to that event. The list of filters that an event supports will be listed in the documentation for that event in the "filters" section.

When matching URLs (as in the example above), event filters support the same URL matching capabilities as expressible with a `events.UrlFilter`, except for scheme and port matching.

## Types

### Event

An object which allows the addition and removal of listeners for a Chrome event.

#### Properties

* `addListener`

  `void`

  Registers an event listener `callback` to an event.

  The `addListener` `function` looks like:

  ```
  (callback: H) => {...}
  ```

  + `callback`

    `H`

    Called when an event occurs. The parameters of this `function` depend on the type of event.
* `addRules`

  `void`

  Registers rules to handle events.

  The `addRules` `function` looks like:

  ```
  (rules: Rule<anyany>[], callback?: function) => {...}
  ```

  + `rules`

    `Rule<anyany>[]`

    Rules to be registered. These do not replace previously registered rules.
  + `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (rules: Rule<anyany>[]) => void
    ```

    - `rules`

      `Rule<anyany>[]`

      Rules that were registered, the optional parameters are filled with values.
* `getRules`

  `void`

  Returns currently registered rules.

  The `getRules` `function` looks like:

  ```
  (ruleIdentifiers?: string[], callback: function) => {...}
  ```

  + `ruleIdentifiers`

    `string[]` optional

    If an array is passed, only rules with identifiers contained in this array are returned.
  + `callback`

    `function`

    The `callback` parameter looks like:

    ```
    (rules: Rule<anyany>[]) => void
    ```

    - `rules`

      `Rule<anyany>[]`

      Rules that were registered, the optional parameters are filled with values.
* `hasListener`

  `void`

  The `hasListener` `function` looks like:

  ```
  (callback: H) => {...}
  ```

  + `callback`

    `H`

    Listener whose registration status shall be tested.

  + returns

    `boolean`

    `True` if `callback` is registered to the event.
* `hasListeners`

  `void`

  The `hasListeners` `function` looks like:

  ```
  () => {...}
  ```

  + returns

    `boolean`

    `True` if any event listeners are registered to the event.
* `removeListener`

  `void`

  Deregisters an event listener `callback` from an event.

  The `removeListener` `function` looks like:

  ```
  (callback: H) => {...}
  ```

  + `callback`

    `H`

    Listener that shall be unregistered.
* `removeRules`

  `void`

  Unregisters currently registered rules.

  The `removeRules` `function` looks like:

  ```
  (ruleIdentifiers?: string[], callback?: function) => {...}
  ```

  + `ruleIdentifiers`

    `string[]` optional

    If an array is passed, only rules with identifiers contained in this array are unregistered.
  + `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    () => void
    ```

### Rule

Description of a declarative rule for handling events.

#### Properties

* `actions`

  `any[]`

  List of actions that are triggered if one of the conditions is fulfilled.
* `conditions`

  `any[]`

  List of conditions that can trigger the actions.
* `id`

  `string` optional

  Optional `identifier` that allows referencing this rule.
* `priority`

  `number` optional

  Optional `priority` of this rule. Defaults to 100.
* `tags`

  `string[]` optional

  Tags can be used to annotate rules and perform operations on sets of rules.

### UrlFilter

Filters URLs for various criteria. See event filtering. All criteria are case sensitive.

#### Properties

* `cidrBlocks`

  `string[]` optional

  Chrome 123+

  Matches if the host part of the URL is an IP address and is contained in any of the CIDR blocks specified in the array.
* `hostContains`

  `string` optional

  Matches if the `host name` of the URL contains a specified `string`. To test whether a `host name` component has a prefix 'foo', use `hostContains: '.foo'`. This matches 'www.foobar.com' and 'foo.com', because an implicit dot is added at the beginning of the `host name`. Similarly, `hostContains` can be used to match against component suffix ('foo.') and to exactly match against components ('.foo.'). Suffix- and exact-matching for the last components need to be done separately using `hostSuffix`, because no implicit dot is added at the end of the `host name`.
* `hostEquals`

  `string` optional

  Matches if the `host name` of the URL is equal to a specified `string`.
* `hostPrefix`

  `string` optional

  Matches if the `host name` of the URL starts with a specified `string`.
* `hostSuffix`

  `string` optional

  Matches if the `host name` of the URL ends with a specified `string`.
* `originAndPathMatches`

  `string` optional

  Matches if the URL without query segment and fragment `identifier` matches a specified regular expression. Port numbers are stripped from the URL if they match the default port number. The regular expressions use the RE2 syntax.
* `pathContains`

  `string` optional

  Matches if the path segment of the URL contains a specified `string`.
* `pathEquals`

  `string` optional

  Matches if the path segment of the URL is equal to a specified `string`.
* `pathPrefix`

  `string` optional

  Matches if the path segment of the URL starts with a specified `string`.
* `pathSuffix`

  `string` optional

  Matches if the path segment of the URL ends with a specified `string`.
* `ports`

  `(number | number[])[]` optional

  Matches if the port of the URL is contained in any of the specified port lists. For example `[80, 443, [1000, 1200]]` matches all requests on port 80, 443 and in the range 1000-1200.
* `queryContains`

  `string` optional

  Matches if the query segment of the URL contains a specified `string`.
* `queryEquals`

  `string` optional

  Matches if the query segment of the URL is equal to a specified `string`.
* `queryPrefix`

  `string` optional

  Matches if the query segment of the URL starts with a specified `string`.
* `querySuffix`

  `string` optional

  Matches if the query segment of the URL ends with a specified `string`.
* `schemes`

  `string[]` optional

  Matches if the scheme of the URL is equal to any of the schemes specified in the array.
* `urlContains`

  `string` optional

  Matches if the URL (without fragment `identifier`) contains a specified `string`. Port numbers are stripped from the URL if they match the default port number.
* `urlEquals`

  `string` optional

  Matches if the URL (without fragment `identifier`) is equal to a specified `string`. Port numbers are stripped from the URL if they match the default port number.
* `urlMatches`

  `string` optional

  Matches if the URL (without fragment `identifier`) matches a specified regular expression. Port numbers are stripped from the URL if they match the default port number. The regular expressions use the RE2 syntax.
* `urlPrefix`

  `string` optional

  Matches if the URL (without fragment `identifier`) starts with a specified `string`. Port numbers are stripped from the URL if they match the default port number.
* `urlSuffix`

  `string` optional

  Matches if the URL (without fragment `identifier`) ends with a specified `string`. Port numbers are stripped from the URL if they match the default port number.

===

---
title: chrome.extension
url: https://developer.chrome.com/docs/extensions/reference/api/extension
---
## Description

The `chrome.extension` API has utilities that can be used by any extension page. It includes support for exchanging messages between an extension and its content scripts or between extensions, as described in detail in Message Passing.

## Types

### ViewType

Chrome 44+

The type of extension view.

#### Enum

*   `"tab"`
*   `"popup"`

## Properties

### inIncognitoContext

`boolean`

True for content scripts running inside incognito tabs, and for extension pages running inside an incognito process. The latter only applies to extensions with 'split' `incognito_behavior`.

## Methods

### getBackgroundPage()

Foreground only

```
chrome.extension.getBackgroundPage()
```

Returns the JavaScript `window` object for the background page running inside the current extension. Returns `null` if the extension has no background page.

#### Returns

*   `Window` | `undefined`

### getViews()

Foreground only

```
chrome.extension.getViews( fetchProperties?: object, )
```

Returns an array of the JavaScript `window` objects for each of the pages running inside the current extension.

#### Parameters

*   `fetchProperties` (`object`, optional)
    *   `tabId` (`number`, optional, Chrome 54+)
        Find a view according to a tab id. If this field is omitted, returns all views.
    *   `type` (`ViewType`, optional)
        The type of view to get. If omitted, returns all views (including background pages and tabs).
    *   `windowId` (`number`, optional)
        The window to restrict the search to. If omitted, returns all views.

#### Returns

*   `Window[]`
    Array of global objects

### isAllowedFileSchemeAccess()

Promise

```
chrome.extension.isAllowedFileSchemeAccess( callback?: function, )
```

Retrieves the state of the extension's access to the `file://` scheme. This corresponds to the user-controlled per-extension 'Allow access to File URLs' setting accessible via the `chrome://extensions` page.

#### Parameters

*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (isAllowedAccess: boolean) => void
    ```
    *   `isAllowedAccess` (`boolean`)
        True if the extension can access the `file://` scheme, false otherwise.

#### Returns

*   `Promise<boolean>` (Chrome 99+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### isAllowedIncognitoAccess()

Promise

```
chrome.extension.isAllowedIncognitoAccess( callback?: function, )
```

Retrieves the state of the extension's access to Incognito-mode. This corresponds to the user-controlled per-extension 'Allowed in Incognito' setting accessible via the `chrome://extensions` page.

#### Parameters

*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (isAllowedAccess: boolean) => void
    ```
    *   `isAllowedAccess` (`boolean`)
        True if the extension has access to Incognito mode, false otherwise.

#### Returns

*   `Promise<boolean>` (Chrome 99+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setUpdateUrlData()

```
chrome.extension.setUpdateUrlData( data: string, )
```

Sets the value of the `ap` CGI parameter used in the extension's update URL. This value is ignored for extensions that are hosted in the Chrome Extension Gallery.

#### Parameters

*   `data` (`string`)

## Events

===

---
title: chrome.extensionTypes
url: https://developer.chrome.com/docs/extensions/reference/api/extensionTypes
---
## Description

The `chrome.extensionTypes` API contains type declarations for Chrome extensions.

## Types

### CSSOrigin

Chrome 66+

The origin of injected CSS.

#### Enum

*   `"author"`
*   `"user"`

### DeleteInjectionDetails

Chrome 87+

Details of the CSS to remove. Either the `code` or the `file` property must be set, but both may not be set at the same time.

#### Properties

*   `allFrames` (`boolean`, optional)
    If `allFrames` is true, implies that the CSS should be removed from all frames of current page. By default, it's `false` and is only removed from the top frame. If `true` and `frameId` is set, then the code is removed from the selected frame and all of its child frames.
*   `code` (`string`, optional)
    CSS code to remove.
*   `cssOrigin` (`CSSOrigin`, optional)
    The origin of the CSS to remove. Defaults to `"author"`.
*   `file` (`string`, optional)
    CSS file to remove.
*   `frameId` (`number`, optional)
    The frame from where the CSS should be removed. Defaults to `0` (the top-level frame).
*   `matchAboutBlank` (`boolean`, optional)
    If `matchAboutBlank` is true, then the code is also removed from `about:blank` and `about:srcdoc` frames if your extension has access to its parent document. By default it is `false`.

### DocumentLifecycle

Chrome 106+

The document lifecycle of the frame.

#### Enum

*   `"prerender"`
*   `"active"`
*   `"cached"`
*   `"pending_deletion"`

### ExecutionWorld

Chrome 111+

The JavaScript world for a script to execute within. Can either be an isolated world unique to this extension, the main world of the DOM which is shared with the page's JavaScript, or a user scripts world that is only available for scripts registered with the User Scripts API.

#### Enum

*   `"ISOLATED"`
*   `"MAIN"`
*   `"USER_SCRIPT"`

### FrameType

Chrome 106+

The type of frame.

#### Enum

*   `"outermost_frame"`
*   `"fenced_frame"`
*   `"sub_frame"`

### ImageDetails

Details about the format and quality of an image.

#### Properties

*   `format` (`ImageFormat`, optional)
    The format of the resulting image. Default is `"jpeg"`.
*   `quality` (`number`, optional)
    When `format` is `"jpeg"`, controls the quality of the resulting image. This value is ignored for PNG images. As quality is decreased, the resulting image will have more visual artifacts, and the number of bytes needed to store it will decrease.

### ImageFormat

Chrome 44+

The format of an image.

#### Enum

*   `"jpeg"`
*   `"png"`

### InjectDetails

Details of the script or CSS to inject. Either the `code` or the `file` property must be set, but both may not be set at the same time.

#### Properties

*   `allFrames` (`boolean`, optional)
    If `allFrames` is true, implies that the JavaScript or CSS should be injected into all frames of current page. By default, it's `false` and is only injected into the top frame. If `true` and `frameId` is set, then the code is inserted in the selected frame and all of its child frames.
*   `code` (`string`, optional)
    JavaScript or CSS code to inject.
    **Warning**: Be careful using the `code` parameter. Incorrect use of it may open your extension to cross site scripting attacks.
*   `cssOrigin` (`CSSOrigin`, optional, Chrome 66+)
    The origin of the CSS to inject. This may only be specified for CSS, not JavaScript. Defaults to `"author"`.
*   `file` (`string`, optional)
    JavaScript or CSS file to inject.
*   `frameId` (`number`, optional, Chrome 50+)
    The frame where the script or CSS should be injected. Defaults to `0` (the top-level frame).
*   `matchAboutBlank` (`boolean`, optional)
    If `matchAboutBlank` is true, then the code is also injected in `about:blank` and `about:srcdoc` frames if your extension has access to its parent document. Code cannot be inserted in top-level `about:`-frames. By default it is `false`.
*   `runAt` (`RunAt`, optional)
    The soonest that the JavaScript or CSS will be injected into the tab. Defaults to `"document_idle"`.

### RunAt

Chrome 44+

The soonest that the JavaScript or CSS will be injected into the tab.

#### Enum

*   `"document_start"`: Script is injected after any files from `css`, but before any other DOM is constructed or any other script is run.
*   `"document_end"`: Script is injected immediately after the DOM is complete, but before subresources like images and frames have loaded.
*   `"document_idle"`: The browser chooses a time to inject the script between `"document_end"` and immediately after the `window.onload` event fires. The exact moment of injection depends on how complex the document is and how long it is taking to load, and is optimized for page load speed. Content scripts running at `"document_idle"` don't need to listen for the `window.onload` event; they are guaranteed to run after the DOM completes. If a script definitely needs to run after `window.onload`, the extension can check if `onload` has already fired by using the `document.readyState` property.

===

---
title: chrome.fileBrowserHandler
url: https://developer.chrome.com/docs/extensions/reference/api/fileBrowserHandler
---
**Important: This API works only on ChromeOS.**

## Description

Use the `chrome.fileBrowserHandler` API to extend the Chrome OS file browser. For example, you can use this API to enable users to upload files to your website.

## Concepts and usage

The ChromeOS file browser comes up when the user either presses `Alt+Shift+M` or connects an external storage device, such as an SD card, USB key, external drive, or digital camera. Besides showing the files on external devices, the file browser can also display files that the user has previously saved to the system.

When the user selects one or more files, the file browser adds buttons representing the valid handlers for those files. For example, in the following screenshot, selecting a file with a `.png` suffix results in an "Save to Gallery" button that the user can click.

## Permissions

`fileBrowserHandler`

You must declare the `"fileBrowserHandler"` permission in the extension manifest.

## Availability

ChromeOS only Foreground only

You must use the `"file_browser_handlers"` field to register the extension as a handler of at least one file type. You should also provide a 16 by 16 icon to be displayed on the button. For example:

```json
{
  "name": "My extension",
  ...
  "file_browser_handlers": [
    {
      "id": "upload",
      "default_title": "Save to Gallery", // What the button will display
      "file_filters": [
        "filesystem:*.jpg", // To match all files, use "filesystem:*.*"
        "filesystem:*.jpeg",
        "filesystem:*.png"
      ]
    }
  ],
  "permissions" : [
    "fileBrowserHandler"
  ],
  "icons": {
    "16": "icon16.png",
    "48": "icon48.png",
    "128": "icon128.png"
  },
  ...
}
```

**Note**: You can specify locale-specific strings for the value of `"default_title"`. See Internationalization (i18n) for details.

### Implement a file browser handler

To use this API, you must implement a function that handles the `onExecute` event of `chrome.fileBrowserHandler`. Your function will be called whenever the user clicks the button that represents your file browser handler. In your function, use the File System API to get access to the file contents. Here is an example:

```javascript
chrome.fileBrowserHandler.onExecute.addListener(async (id, details) => {
  if (id !== 'upload') {
    return; // check if you have multiple file_browser_handlers
  }
  for (const entry of details.entries) {
    // the FileSystemFileEntry doesn't have a Promise API, wrap in one
    const file = await new Promise((resolve, reject) => {
      entry.file(resolve, reject);
    });
    const buffer = await file.arrayBuffer();
    // do something with buffer
  }
});
```

Your event handler is passed two arguments:

*   `id`: The `id` value from the manifest file. If your extension implements multiple handlers, you can check the `id` value to see which handler has been triggered.
*   `details`: An object describing the event. You can get the file or files that the user has selected from the `entries` field of this object, which is an array of `FileSystemFileEntry` objects.

## Types

### FileHandlerExecuteEventDetails

Event details payload for `fileBrowserHandler.onExecute` event.

#### Properties

*   `entries` (`any[]`)
    Array of `Entry` instances representing files that are targets of this action (selected in ChromeOS file browser).
*   `tab_id` (`number`, optional)
    The ID of the tab that raised this event. Tab IDs are unique within a browser session.

## Events

### onExecute

```
chrome.fileBrowserHandler.onExecute.addListener( callback: function, )
```

Fired when file system action is executed from ChromeOS file browser.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (id: string, details: FileHandlerExecuteEventDetails) => void
    ```
    *   `id` (`string`)
    *   `details` (`FileHandlerExecuteEventDetails`)

===

---
title: chrome.fileSystemProvider
url: https://developer.chrome.com/docs/extensions/reference/api/fileSystemProvider
---
**Important: This API works only on ChromeOS.**

## Description

Use the `chrome.fileSystemProvider` API to create file systems, that can be accessible from the file manager on Chrome OS.

## Permissions

`fileSystemProvider`

## Availability

ChromeOS only

You must declare the `"fileSystemProvider"` permission and section in the extension manifest to use the File System Provider API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "fileSystemProvider"
  ],
  ...
  "file_system_provider_capabilities": {
    "configurable": true,
    "watchable": false,
    "multiple_mounts": true,
    "source": "network"
  },
  ...
}
```

The `file_system_provider` section must be declared as follows:

*   `configurable` (`boolean`, optional) - Whether configuring via `onConfigureRequested` is supported. By default: `false`.
*   `multiple_mounts` (`boolean`, optional) - Whether multiple (more than one) mounted file systems are supported. By default: `false`.
*   `watchable` (`boolean`, optional) - Whether setting watchers and notifying about changes is supported. By default: `false`.
*   `source` (enum of `"file"`, `"device"`, or `"network"`, required) - Source of data for mounted file systems.

Files app uses above information in order to render related UI elements appropriately. For example, if `configurable` is set to `true`, then a menu item for configuring volumes will be rendered. Similarly, if `multiple_mounts` is set to `true`, then Files app will allow to add more than one mount points from the UI. If `watchable` is `false`, then a refresh button will be rendered. Note, that if possible you should add support for watchers, so changes on the file system can be reflected immediately and automatically.

## Overview

File System Provider API allows extensions to support virtual file systems, which are available in the file manager on ChromeOS. Use cases include decompressing archives and accessing files in a cloud service other than Drive.

## Mounting file systems

Providing extensions can either provide file system contents from an external source (such as a remote server or a USB device), or using a local file (such as an archive) as its input.

In order to write file systems which are file handlers (source is `"file"`) the provider must be a packaged app, as the `onLaunched` event is not available to extensions.

If the source is `network` or a `device`, then the file system should be mounted when `onMountRequested` event is called.

| Source of the file system data | Entry point |
| --- | --- |
| `"file"` | Available to packaged apps only. |
| `"device"` or `"network"` | `onMountRequested` |

## Configuring file systems

Provided file systems once mounted can be configured via the `onConfigureRequested` event. It's especially useful for file systems which provide contents via network in order to set proper credentials. Handling this event is optional.

## Life cycle

Provided file systems once mounted are remembered by Chrome and remounted automatically after reboot or restart. Hence, once a file system is mounted by a providing extension, it will stay until either the extension is unloaded, or the extension calls the `unmount` method.

## Types

### AbortRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `operationRequestId` (`number`)
    An ID of the request to be aborted.
*   `requestId` (`number`)
    The unique identifier of this request.

### Action

Chrome 45+

#### Properties

*   `id` (`string`)
    The identifier of the action. Any string or `CommonActionId` for common actions.
*   `title` (`string`, optional)
    The title of the action. It may be ignored for common actions.

### AddWatcherRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the entry to be observed.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether observing should include all child entries recursively. It can be `true` for directories only.
*   `requestId` (`number`)
    The unique identifier of this request.

### Change

#### Properties

*   `changeType` (`ChangeType`)
    The type of the change which happened to the entry.
*   `cloudFileInfo` (`CloudFileInfo`, optional, Chrome 125+)
    Information relating to the file if backed by a cloud file system.
*   `entryPath` (`string`)
    The path of the changed entry.

### ChangeType

Type of a change detected on the observed directory.

#### Enum

*   `"CHANGED"`
*   `"DELETED"`

### CloseFileRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

### CloudFileInfo

Chrome 125+

#### Properties

*   `versionTag` (`string`, optional)
    A tag that represents the version of the file.

### CloudIdentifier

Chrome 117+

#### Properties

*   `id` (`string`)
    The provider's identifier for the given file/directory.
*   `providerName` (`string`)
    Identifier for the cloud storage provider (e.g. `'drive.google.com'`).

### CommonActionId

Chrome 45+

List of common actions. `"SHARE"` is for sharing files with others. `"SAVE_FOR_OFFLINE"` for pinning (saving for offline access). `"OFFLINE_NOT_NECESSARY"` for notifying that the file doesn't need to be stored for offline access anymore. Used by `onGetActionsRequested` and `onExecuteActionRequested`.

#### Enum

*   `"SAVE_FOR_OFFLINE"`
*   `"OFFLINE_NOT_NECESSARY"`
*   `"SHARE"`

### ConfigureRequestedOptions

Chrome 44+

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be configured.
*   `requestId` (`number`)
    The unique identifier of this request.

### CopyEntryRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `sourcePath` (`string`)
    The source path of the entry to be copied.
*   `targetPath` (`string`)
    The destination path for the copy operation.

### CreateDirectoryRequestedOptions

#### Properties

*   `directoryPath` (`string`)
    The path of the directory to be created.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether the operation is recursive (for directories only).
*   `requestId` (`number`)
    The unique identifier of this request.

### CreateFileRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be created.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### DeleteEntryRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the entry to be deleted.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether the operation is recursive (for directories only).
*   `requestId` (`number`)
    The unique identifier of this request.

### EntryMetadata

#### Properties

*   `cloudFileInfo` (`CloudFileInfo`, optional, Chrome 125+)
    Information that identifies a specific file in the underlying cloud file system. Must be provided if requested in options and the file is backed by cloud storage.
*   `cloudIdentifier` (`CloudIdentifier`, optional, Chrome 117+)
    Cloud storage representation of this entry. Must be provided if requested in options and the file is backed by cloud storage. For local files not backed by cloud storage, it should be `undefined` when requested.
*   `isDirectory` (`boolean`, optional)
    `true` if it is a directory. Must be provided if requested in options.
*   `mimeType` (`string`, optional)
    Mime type for the entry. Always optional, but should be provided if requested in options.
*   `modificationTime` (`Date`, optional)
    The last modified time of this entry. Must be provided if requested in options.
*   `name` (`string`, optional)
    Name of this entry (not full path name). Must not contain `'/'`. For root it must be empty. Must be provided if requested in options.
*   `size` (`number`, optional)
    File size in bytes. Must be provided if requested in options.
*   `thumbnail` (`string`, optional)
    Thumbnail image as a data URI in either PNG, JPEG or WEBP format, at most 32 KB in size. Optional, but can be provided only when explicitly requested by the `onGetMetadataRequested` event.

### ExecuteActionRequestedOptions

Chrome 45+

#### Properties

*   `actionId` (`string`)
    The identifier of the action to be executed.
*   `entryPaths` (`string[]`, Chrome 47+)
    The set of paths of the entries to be used for the action.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### FileSystemInfo

#### Properties

*   `displayName` (`string`)
    A human-readable name for the file system.
*   `fileSystemId` (`string`)
    The identifier of the file system.
*   `openedFiles` (`OpenedFile[]`)
    List of currently opened files.
*   `openedFilesLimit` (`number`)
    The maximum number of files that can be opened at once. If `0`, then not limited.
*   `supportsNotifyTag` (`boolean`, optional, Chrome 45+)
    Whether the file system supports the `tag` field for observing directories.
*   `watchers` (`Watcher[]`, Chrome 45+)
    List of watchers.
*   `writable` (`boolean`)
    Whether the file system supports operations which may change contents of the file system (such as creating, deleting or writing to files).

### GetActionsRequestedOptions

Chrome 45+

#### Properties

*   `entryPaths` (`string[]`, Chrome 47+)
    List of paths of entries for the list of actions.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### GetMetadataRequestedOptions

#### Properties

*   `cloudFileInfo` (`boolean`, Chrome 125+)
    Set to `true` if `cloudFileInfo` value is requested.
*   `cloudIdentifier` (`boolean`, Chrome 117+)
    Set to `true` if `cloudIdentifier` value is requested.
*   `entryPath` (`string`)
    The path of the entry to fetch metadata about.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `isDirectory` (`boolean`, Chrome 49+)
    Set to `true` if `is_directory` value is requested.
*   `mimeType` (`boolean`, Chrome 49+)
    Set to `true` if `mimeType` value is requested.
*   `modificationTime` (`boolean`, Chrome 49+)
    Set to `true` if `modificationTime` value is requested.
*   `name` (`boolean`, Chrome 49+)
    Set to `true` if `name` value is requested.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `size` (`boolean`, Chrome 49+)
    Set to `true` if `size` value is requested.
*   `thumbnail` (`boolean`)
    Set to `true` if `thumbnail` value is requested.

### MountOptions

#### Properties

*   `displayName` (`string`)
    A human-readable name for the file system.
*   `fileSystemId` (`string`)
    The string indentifier of the file system. Must be unique per each extension.
*   `openedFilesLimit` (`number`, optional)
    The maximum number of files that can be opened at once. If not specified, or `0`, then not limited.
*   `persistent` (`boolean`, optional, Chrome 64+)
    Whether the framework should resume the file system at the next sign-in session. `true` by default.
*   `supportsNotifyTag` (`boolean`, optional, Chrome 45+)
    Whether the file system supports the `tag` field for observed directories.
*   `writable` (`boolean`, optional)
    Whether the file system supports operations which may change contents of the file system (such as creating, deleting or writing to files).

### MoveEntryRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `sourcePath` (`string`)
    The source path of the entry to be moved into a new place.
*   `targetPath` (`string`)
    The destination path for the copy operation.

### NotifyOptions

#### Properties

*   `changeType` (`ChangeType`)
    The type of the change which happened to the observed entry. If it is `DELETED`, then the observed entry will be automatically removed from the list of observed entries.
*   `changes` (`Change[]`, optional)
    List of changes to entries within the observed directory (including the entry itself)
*   `fileSystemId` (`string`)
    The identifier of the file system related to this change.
*   `observedPath` (`string`)
    The path of the observed entry.
*   `recursive` (`boolean`)
    Mode of the observed entry.
*   `tag` (`string`, optional)
    Tag for the notification. Required if the file system was mounted with the `supportsNotifyTag` option. Note, that this flag is necessary to provide notifications about changes which changed even when the system was shutdown.

### OpenedFile

#### Properties

*   `filePath` (`string`)
    The path of the opened file.
*   `mode` (`OpenFileMode`)
    Whether the file was opened for reading or writing.
*   `openRequestId` (`number`)
    A request ID to be be used by consecutive read/write and close requests.

### OpenFileMode

Mode of opening a file. Used by `onOpenFileRequested`.

#### Enum

*   `"READ"`
*   `"WRITE"`

### OpenFileRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be opened.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `mode` (`OpenFileMode`)
    Whether the file will be used for reading or writing.
*   `requestId` (`number`)
    A request ID which will be used by consecutive read/write and close requests.

### ProviderError

Error codes used by providing extensions in response to requests as well as in case of errors when calling methods of the API. For success, `"OK"` must be used.

#### Enum

*   `"OK"`
*   `"FAILED"`
*   `"IN_USE"`
*   `"EXISTS"`
*   `"NOT_FOUND"`
*   `"ACCESS_DENIED"`
*   `"TOO_MANY_OPENED"`
*   `"NO_MEMORY"`
*   `"NO_SPACE"`
*   `"NOT_A_DIRECTORY"`
*   `"INVALID_OPERATION"`
*   `"SECURITY"`
*   `"ABORT"`
*   `"NOT_A_FILE"`
*   `"NOT_EMPTY"`
*   `"INVALID_URL"`
*   `"IO"`

### ReadDirectoryRequestedOptions

#### Properties

*   `directoryPath` (`string`)
    The path of the directory which contents are requested.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `isDirectory` (`boolean`, Chrome 49+)
    Set to `true` if `is_directory` value is requested.
*   `mimeType` (`boolean`, Chrome 49+)
    Set to `true` if `mimeType` value is requested.
*   `modificationTime` (`boolean`, Chrome 49+)
    Set to `true` if `modificationTime` value is requested.
*   `name` (`boolean`, Chrome 49+)
    Set to `true` if `name` value is requested.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `size` (`boolean`, Chrome 49+)
    Set to `true` if `size` value is requested.
*   `thumbnail` (`boolean`, Chrome 49+)
    Set to `true` if `thumbnail` value is requested.

### ReadFileRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `length` (`number`)
    Number of bytes to be returned.
*   `offset` (`number`)
    Position in the file (in bytes) to start reading from.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

### RemoveWatcherRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the watched entry.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Mode of the watcher.
*   `requestId` (`number`)
    The unique identifier of this request.

### TruncateRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be truncated.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `length` (`number`)
    Number of bytes to be retained after the operation completes.
*   `requestId` (`number`)
    The unique identifier of this request.

### UnmountOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be unmounted.

### UnmountRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be unmounted.
*   `requestId` (`number`)
    The unique identifier of this request.

### Watcher

#### Properties

*   `entryPath` (`string`)
    The path of the entry being observed.
*   `lastTag` (`string`, optional)
    Tag used by the last notification for the watcher.
*   `recursive` (`boolean`)
    Whether watching should include all child entries recursively. It can be `true` for directories only.

### WriteFileRequestedOptions

#### Properties

*   `data` (`ArrayBuffer`)
    Buffer of bytes to be written to the file.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `offset` (`number`)
    Position in the file (in bytes) to start writing the bytes from.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

## Methods

### get()

Promise

```
chrome.fileSystemProvider.get( fileSystemId: string, callback?: function, )
```

Returns information about a file system with the passed `fileSystemId`.

#### Parameters

*   `fileSystemId` (`string`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (fileSystem: FileSystemInfo) => void
    ```
    *   `fileSystem` (`FileSystemInfo`)

#### Returns

*   `Promise<FileSystemInfo>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAll()

Promise

```
chrome.fileSystemProvider.getAll( callback?: function, )
```

Returns all file systems mounted by the extension.

#### Parameters

*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (fileSystems: FileSystemInfo[]) => void
    ```
    *   `fileSystems` (`FileSystemInfo[]`)

#### Returns

*   `Promise<FileSystemInfo[]>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### mount()

Promise

```
chrome.fileSystemProvider.mount( options: MountOptions, callback?: function, )
```

Mounts a file system with the given `options`.

#### Parameters

*   `options` (`MountOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### notify()

Promise

```
chrome.fileSystemProvider.notify( options: NotifyOptions, callback?: function, )
```

Notifies about a change in the watched directory.

#### Parameters

*   `options` (`NotifyOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### unmount()

Promise

```
chrome.fileSystemProvider.unmount( options: UnmountOptions, callback?: function, )
```

Unmounts a file system with the given `fileSystemId`.

#### Parameters

*   `options` (`UnmountOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onAbortRequested

```
chrome.fileSystemProvider.onAbortRequested.addListener(
  callback: (options: AbortRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to abort an operation is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: AbortRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`AbortRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onAddWatcherRequested

```
chrome.fileSystemProvider.onAddWatcherRequested.addListener(
  callback: (options: AddWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to add a new watcher is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: AddWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`AddWatcherRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCloseFileRequested

```
chrome.fileSystemProvider.onCloseFileRequested.addListener(
  callback: (options: CloseFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to close a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CloseFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CloseFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onConfigureRequested

Chrome 44+

```
chrome.fileSystemProvider.onConfigureRequested.addListener(
  callback: (options: ConfigureRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to configure a mounted file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ConfigureRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`ConfigureRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCopyEntryRequested

```
chrome.fileSystemProvider.onCopyEntryRequested.addListener(
  callback: (options: CopyEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to copy an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CopyEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CopyEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCreateDirectoryRequested

```
chrome.fileSystemProvider.onCreateDirectoryRequested.addListener(
  callback: (options: CreateDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to create a directory is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CreateDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CreateDirectoryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCreateFileRequested

```
chrome.fileSystemProvider.onCreateFileRequested.addListener(
  callback: (options: CreateFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to create a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CreateFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CreateFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onDeleteEntryRequested

```
chrome.fileSystemProvider.onDeleteEntryRequested.addListener(
  callback: (options: DeleteEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to delete an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: DeleteEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`DeleteEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onExecuteActionRequested

Chrome 45+

```
chrome.fileSystemProvider.onExecuteActionRequested.addListener(
  callback: (options: ExecuteActionRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to execute an action is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ExecuteActionRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`ExecuteActionRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onGetActionsRequested

Chrome 45+

```
chrome.fileSystemProvider.onGetActionsRequested.addListener(
  callback: (options: GetActionsRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to get a list of actions for a set of entries is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: GetActionsRequestedOptions, successCallback: (actions: Action[]) => void, errorCallback: function) => void
    ```
    *   `options` (`GetActionsRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (actions: Action[]) => void
        ```
        *   `actions` (`Action[]`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onGetMetadataRequested

```
chrome.fileSystemProvider.onGetMetadataRequested.addListener(
  callback: (options: GetMetadataRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to get metadata of an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: GetMetadataRequestedOptions, successCallback: (metadata: EntryMetadata) => void, errorCallback: function) => void
    ```
    *   `options` (`GetMetadataRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (metadata: EntryMetadata) => void
        ```
        *   `metadata` (`EntryMetadata`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onMountRequested

Chrome 44+

```
chrome.fileSystemProvider.onMountRequested.addListener(
  callback: (successCallback: function, errorCallback: function) => void
)
```

Raised when a request to mount a new file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (successCallback: function, errorCallback: function) => void
    ```
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onMoveEntryRequested

```
chrome.fileSystemProvider.onMoveEntryRequested.addListener(
  callback: (options: MoveEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to move an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: MoveEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`MoveEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onOpenFileRequested

```
chrome.fileSystemProvider.onOpenFileRequested.addListener(
  callback: (options: OpenFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to open a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: OpenFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`OpenFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onReadDirectoryRequested

```
chrome.fileSystemProvider.onReadDirectoryRequested.addListener(
  callback: (options: ReadDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to read a directory is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ReadDirectoryRequestedOptions, successCallback: (entries: EntryMetadata[], hasMore: boolean) => void, errorCallback: function) => void
    ```
    *   `options` (`ReadDirectoryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (entries: EntryMetadata[], hasMore: boolean) => void
        ```
        *   `entries` (`EntryMetadata[]`)
        *   `hasMore` (`boolean`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onReadFileRequested

```
chrome.fileSystemProvider.onReadFileRequested.addListener(
  callback: (options: ReadFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to read a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ReadFileRequestedOptions, successCallback: (data: ArrayBuffer, hasMore: boolean) => void, errorCallback: function) => void
    ```
    *   `options` (`ReadFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (data: ArrayBuffer, hasMore: boolean) => void
        ```
        *   `data` (`ArrayBuffer`)
        *   `hasMore` (`boolean`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onRemoveWatcherRequested

```
chrome.fileSystemProvider.onRemoveWatcherRequested.addListener(
  callback: (options: RemoveWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to remove a watcher is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: RemoveWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`RemoveWatcherRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onTruncateRequested

```
chrome.fileSystemProvider.onTruncateRequested.addListener(
  callback: (options: TruncateRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to truncate a file to a new size is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: TruncateRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`TruncateRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onUnmountRequested

```
chrome.fileSystemProvider.onUnmountRequested.addListener(
  callback: (options: UnmountRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to unmount a file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: UnmountRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`UnmountRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onWriteFileRequested

```
chrome.fileSystemProvider.onWriteFileRequested.addListener(
  callback: (options: WriteFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to write to a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: WriteFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`WriteFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

===

---
title: chrome.fontSettings
url: https://developer.chrome.com/docs/extensions/reference/api/fontSettings
---

# chrome.fontSettings

## Description

Use the `chrome.fontSettings` API to manage Chrome's font settings.

## Permissions

`fontSettings`

To use the Font Settings API, you must declare the "`fontSettings`" permission in the extension manifest. For example:

```json
{
  "name": "My Font Settings Extension",
  "description": "Customize your fonts",
  "version": "0.2",
  "permissions": [
    "fontSettings"
  ],
  ...
}
```

## Concepts and usage

Chrome allows for some font settings to depend on certain generic font families and language scripts. For example, the font used for sans-serif Simplified Chinese may be different than the font used for serif Japanese.

The generic font families supported by Chrome are based on CSS generic font families and are listed under `GenericReference`. When a web page specifies a generic font family, Chrome selects the font based on the corresponding setting. If no generic font family is specified, Chrome uses the setting for the "standard" generic font family.

When a web page specifies a language, Chrome selects the font based on the setting for the corresponding language script. If no language is specified, Chrome uses the setting for the default, or global, script.

The supported language scripts are specified by ISO 15924 script code and listed under `ScriptCode`. Technically, Chrome settings are not strictly per-script but also depend on language. For example, Chrome chooses the font for Cyrillic (ISO 15924 script code "`Cyrl`") when a web page specifies the Russian language, and uses this font not just for Cyrillic script but for everything the font covers, such as Latin.

## Examples

The following code gets the standard font for Arabic.

```javascript
chrome.fontSettings.getFont(
  { genericFamily: 'standard', script: 'Arab' },
  function(details) {
    console.log(details.fontId);
  }
);
```

The next snippet sets the sans-serif font for Japanese.

```javascript
chrome.fontSettings.setFont(
  {
    genericFamily: 'sansserif',
    script: 'Jpan',
    fontId: 'MS PGothic'
  }
);
```

To try this API, install the `fontSettings` API example from the `chrome-extension-samples` repository.

## Types

### FontName

Represents a font name.

#### Properties

*   `displayName`

    string

    The display name of the font.
*   `fontId`

    string

    The font ID.

### GenericFamily

A CSS generic font family.

#### Enum

*   `"standard"`
*   `"sansserif"`
*   `"serif"`
*   `"fixed"`
*   `"cursive"`
*   `"fantasy"`
*   `"math"`

### LevelOfControl

One of `not_controllable`: cannot be controlled by any extension `controlled_by_other_extensions`: controlled by extensions with higher precedence `controllable_by_this_extension`: can be controlled by this extension `controlled_by_this_extension`: controlled by this extension

#### Enum

*   `"not_controllable"`
*   `"controlled_by_other_extensions"`
*   `"controllable_by_this_extension"`
*   `"controlled_by_this_extension"`

### ScriptCode

An ISO 15924 script code. The default, or global, script is represented by script code `"Zyyy"`.

#### Enum

`"Afak"`, `"Arab"`, `"Armi"`, `"Armn"`, `"Avst"`, `"Bali"`, `"Bamu"`, `"Bass"`, `"Batk"`, `"Beng"`, `"Blis"`, `"Bopo"`, `"Brah"`, `"Brai"`, `"Bugi"`, `"Buhd"`, `"Cakm"`, `"Cans"`, `"Cari"`, `"Cham"`, `"Cher"`, `"Cirt"`, `"Copt"`, `"Cprt"`, `"Cyrl"`, `"Cyrs"`, `"Deva"`, `"Dsrt"`, `"Dupl"`, `"Egyd"`, `"Egyh"`, `"Egyp"`, `"Elba"`, `"Ethi"`, `"Geor"`, `"Geok"`, `"Glag"`, `"Goth"`, `"Gran"`, `"Grek"`, `"Gujr"`, `"Guru"`, `"Hang"`, `"Hani"`, `"Hano"`, `"Hans"`, `"Hant"`, `"Hebr"`, `"Hluw"`, `"Hmng"`, `"Hung"`, `"Inds"`, `"Ital"`, `"Java"`, `"Jpan"`, `"Jurc"`, `"Kali"`, `"Khar"`, `"Khmr"`, `"Khoj"`, `"Knda"`, `"Kpel"`, `"Kthi"`, `"Lana"`, `"Laoo"`, `"Latf"`, `"Latg"`, `"Latn"`, `"Lepc"`, `"Limb"`, `"Lina"`, `"Linb"`, `"Lisu"`, `"Loma"`, `"Lyci"`, `"Lydi"`, `"Mand"`, `"Mani"`, `"Maya"`, `"Mend"`, `"Merc"`, `"Mero"`, `"Mlym"`, `"Moon"`, `"Mong"`, `"Mroo"`, `"Mtei"`, `"Mymr"`, `"Narb"`, `"Nbat"`, `"Nkgb"`, `"Nkoo"`, `"Nshu"`, `"Ogam"`, `"Olck"`, `"Orkh"`, `"Orya"`, `"Osma"`, `"Palm"`, `"Perm"`, `"Phag"`, `"Phli"`, `"Phlp"`, `"Phlv"`, `"Phnx"`, `"Plrd"`, `"Prti"`, `"Rjng"`, `"Roro"`, `"Runr"`, `"Samr"`, `"Sara"`, `"Sarb"`, `"Saur"`, `"Sgnw"`, `"Shaw"`, `"Shrd"`, `"Sind"`, `"Sinh"`, `"Sora"`, `"Sund"`, `"Sylo"`, `"Syrc"`, `"Syre"`, `"Syrj"`, `"Syrn"`, `"Tagb"`, `"Takr"`, `"Tale"`, `"Talu"`, `"Taml"`, `"Tang"`, `"Tavt"`, `"Telu"`, `"Teng"`, `"Tfng"`, `"Tglg"`, `"Thaa"`, `"Thai"`, `"Tibt"`, `"Tirh"`, `"Ugar"`, `"Vaii"`, `"Visp"`, `"Wara"`, `"Wole"`, `"Xpeo"`, `"Xsux"`, `"Yiii"`, `"Zmth"`, `"Zsym"`, `"Zyyy"`

## Methods

### clearDefaultFixedFontSize()

Promise

```javascript
chrome.fontSettings.clearDefaultFixedFontSize(
  details?: object,
  callback?: function,
)
```

Clears the default fixed font size set by this extension, if any.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### clearDefaultFontSize()

Promise

```javascript
chrome.fontSettings.clearDefaultFontSize(
  details?: object,
  callback?: function,
)
```

Clears the default font size set by this extension, if any.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### clearFont()

Promise

```javascript
chrome.fontSettings.clearFont(
  details: object,
  callback?: function,
)
```

Clears the font set by this extension, if any.

#### Parameters

*   `details`

    object

    *   `genericFamily`

        `GenericFamily`

        The generic font family for which the font should be cleared.
    *   `script`

        `ScriptCode` optional

        The script for which the font should be cleared. If omitted, the global script font setting is cleared.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### clearMinimumFontSize()

Promise

```javascript
chrome.fontSettings.clearMinimumFontSize(
  details?: object,
  callback?: function,
)
```

Clears the minimum font size set by this extension, if any.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getDefaultFixedFontSize()

Promise

```javascript
chrome.fontSettings.getDefaultFixedFontSize(
  details?: object,
  callback?: function,
)
```

Gets the default size for fixed width fonts.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

#### Returns

*   `Promise<object>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getDefaultFontSize()

Promise

```javascript
chrome.fontSettings.getDefaultFontSize(
  details?: object,
  callback?: function,
)
```

Gets the default font size.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

#### Returns

*   `Promise<object>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getFont()

Promise

```javascript
chrome.fontSettings.getFont(
  details: object,
  callback?: function,
)
```

Gets the font for a given script and generic font family.

#### Parameters

*   `details`

    object

    *   `genericFamily`

        `GenericFamily`

        The generic font family for which the font should be retrieved.
    *   `script`

        `ScriptCode` optional

        The script for which the font should be retrieved. If omitted, the font setting for the global script (script code `"Zyyy"`) is retrieved.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `fontId`

            string

            The font ID. Rather than the literal font ID preference value, this may be the ID of the font that the system resolves the preference value to. So, `fontId` can differ from the font passed to `setFont`, if, for example, the font is not available on the system. The empty string signifies fallback to the global script font setting.
        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.

#### Returns

*   `Promise<object>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getFontList()

Promise

```javascript
chrome.fontSettings.getFontList(callback?: function)
```

Gets a list of fonts on the system.

#### Parameters

*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (results: FontName[]) => void
    ```

    *   `results`

        `FontName[]`

#### Returns

*   `Promise<FontName[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getMinimumFontSize()

Promise

```javascript
chrome.fontSettings.getMinimumFontSize(
  details?: object,
  callback?: function,
)
```

Gets the minimum font size.

#### Parameters

*   `details`

    object optional

    This parameter is currently unused.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

#### Returns

*   `Promise<object>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setDefaultFixedFontSize()

Promise

```javascript
chrome.fontSettings.setDefaultFixedFontSize(
  details: object,
  callback?: function,
)
```

Sets the default size for fixed width fonts.

#### Parameters

*   `details`

    object

    *   `pixelSize`

        number

        The font size in pixels.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setDefaultFontSize()

Promise

```javascript
chrome.fontSettings.setDefaultFontSize(
  details: object,
  callback?: function,
)
```

Sets the default font size.

#### Parameters

*   `details`

    object

    *   `pixelSize`

        number

        The font size in pixels.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setFont()

Promise

```javascript
chrome.fontSettings.setFont(
  details: object,
  callback?: function,
)
```

Sets the font for a given script and generic font family.

#### Parameters

*   `details`

    object

    *   `fontId`

        string

        The font ID. The empty string means to fallback to the global script font setting.
    *   `genericFamily`

        `GenericFamily`

        The generic font family for which the font should be set.
    *   `script`

        `ScriptCode` optional

        The script code which the font should be set. If omitted, the font setting for the global script (script code `"Zyyy"`) is set.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setMinimumFontSize()

Promise

```javascript
chrome.fontSettings.setMinimumFontSize(
  details: object,
  callback?: function,
)
```

Sets the minimum font size.

#### Parameters

*   `details`

    object

    *   `pixelSize`

        number

        The font size in pixels.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onDefaultFixedFontSizeChanged

```javascript
chrome.fontSettings.onDefaultFixedFontSizeChanged.addListener(
  callback: function,
)
```

Fired when the default fixed font size setting changes.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

### onDefaultFontSizeChanged

```javascript
chrome.fontSettings.onDefaultFontSizeChanged.addListener(
  callback: function,
)
```

Fired when the default font size setting changes.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

### onFontChanged

```javascript
chrome.fontSettings.onFontChanged.addListener(callback: function)
```

Fired when a font setting changes.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `fontId`

            string

            The font ID. See the description in `getFont`.
        *   `genericFamily`

            `GenericFamily`

            The generic font family for which the font setting has changed.
        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `script`

            `ScriptCode` optional

            The script code for which the font setting has changed.

### onMinimumFontSizeChanged

```javascript
chrome.fontSettings.onMinimumFontSizeChanged.addListener(
  callback: function,
)
```

Fired when the minimum font size setting changes.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (details: object) => void
    ```

    *   `details`

        object

        *   `levelOfControl`

            `LevelOfControl`

            The level of control this extension has over the setting.
        *   `pixelSize`

            number

            The font size in pixels.

===

---
title: chrome.gcm
url: https://developer.chrome.com/docs/extensions/reference/api/gcm
---

# chrome.gcm

## Description

Use `chrome.gcm` to enable apps and extensions to send and receive messages through Firebase Cloud Messaging (FCM).

## Permissions

`gcm`

## Properties

### MAX_MESSAGE_SIZE

The maximum size (in bytes) of all key/value pairs in a message.

#### Value

`4096`

## Methods

### register()

Promise

```javascript
chrome.gcm.register(
  senderIds: string[],
  callback?: function,
)
```

Registers the application with FCM. The registration ID will be returned by the callback. If `register` is called again with the same list of `senderIds`, the same registration ID will be returned.

#### Parameters

*   `senderIds`

    string[]

    A list of server IDs that are allowed to send messages to the application. It should contain at least one and no more than 100 sender IDs.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (registrationId: string) => void
    ```

    *   `registrationId`

        string

        A registration ID assigned to the application by the FCM.

#### Returns

*   `Promise<string>`

    Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### send()

Promise

```javascript
chrome.gcm.send(
  message: object,
  callback?: function,
)
```

Sends a message according to its contents.

#### Parameters

*   `message`

    object

    A message to send to the other party via FCM.

    *   `data`

        object

        Message data to send to the server. Case-insensitive `goog.` and `google`, as well as case-sensitive `collapse_key` are disallowed as key prefixes. Sum of all key/value pairs should not exceed `gcm.MAX_MESSAGE_SIZE`.
    *   `destinationId`

        string

        The ID of the server to send the message to as assigned by Google API Console.
    *   `messageId`

        string

        The ID of the message. It must be unique for each message in scope of the applications. See the Cloud Messaging documentation for advice for picking and handling an ID.
    *   `timeToLive`

        number optional

        Time-to-live of the message in seconds. If it is not possible to send the message within that time, an `onSendError` event will be raised. A time-to-live of `0` indicates that the message should be sent immediately or fail if it's not possible. The default value of time-to-live is `86,400` seconds (1 day) and the maximum value is `2,419,200` seconds (28 days).
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (messageId: string) => void
    ```

    *   `messageId`

        string

        The ID of the message that the callback was issued for.

#### Returns

*   `Promise<string>`

    Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### unregister()

Promise

```javascript
chrome.gcm.unregister(callback?: function)
```

Unregisters the application from FCM.

#### Parameters

*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onMessage

```javascript
chrome.gcm.onMessage.addListener(callback: function)
```

Fired when a message is received through FCM.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (message: object) => void
    ```

    *   `message`

        object

        *   `collapseKey`

            string optional

            The collapse key of a message. See the Non-collapsible and collapsible messages for details.
        *   `data`

            object

            The message data.
        *   `from`

            string optional

            The sender who issued the message.

### onMessagesDeleted

```javascript
chrome.gcm.onMessagesDeleted.addListener(callback: function)
```

Fired when a FCM server had to delete messages sent by an app server to the application. See Lifetime of a message for details on handling this event.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    () => void
    ```

### onSendError

```javascript
chrome.gcm.onSendError.addListener(callback: function)
```

Fired when it was not possible to send a message to the FCM server.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (error: object) => void
    ```

    *   `error`

        object

        *   `details`

            object

            Additional details related to the error, when available.
        *   `errorMessage`

            string

            The error message describing the problem.
        *   `messageId`

            string optional

            The ID of the message with this error, if error is related to a specific message.

===

---
title: chrome.history
url: https://developer.chrome.com/docs/extensions/reference/api/history
---

# chrome.history

## Description

Use the `chrome.history` API to interact with the browser's record of visited pages. You can add, remove, and query for URLs in the browser's history. To override the history page with your own version, see Override Pages.

## Permissions

`history`

To interact with the user's browser history, use the history API.

To use the history API, declare the "`history`" permission in the extension manifest. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "history"
  ],
  ...
}
```

## Concepts and usage

### Transition types

The history API uses transition types to describe how the browser navigated to a particular URL on a particular visit. For example, if a user visits a page by clicking a link on another page, the transition type is "`link`". See the reference content for a list of transition types.

## Examples

To try this API, install the history API example from the `chrome-extension-samples` repository.

## Types

### HistoryItem

An object encapsulating one result of a history query.

#### Properties

*   `id`

    string

    The unique identifier for the item.
*   `lastVisitTime`

    number optional

    When this page was last loaded, represented in milliseconds since the epoch.
*   `title`

    string optional

    The title of the page when it was last loaded.
*   `typedCount`

    number optional

    The number of times the user has navigated to this page by typing in the address.
*   `url`

    string optional

    The URL navigated to by a user.
*   `visitCount`

    number optional

    The number of times the user has navigated to this page.

### TransitionType

Chrome 44+

The transition type for this visit from its referrer.

#### Enum

*   `"link"` The user arrived at this page by clicking a link on another page.
*   `"typed"` The user arrived at this page by typing the URL in the address bar. This is also used for other explicit navigation actions.
*   `"auto_bookmark"` The user arrived at this page through a suggestion in the UI, for example, through a menu item.
*   `"auto_subframe"` The user arrived at this page through subframe navigation that they didn't request, such as through an ad loading in a frame on the previous page. These don't always generate new navigation entries in the back and forward menus.
*   `"manual_subframe"` The user arrived at this page by selecting something in a subframe.
*   `"generated"` The user arrived at this page by typing in the address bar and selecting an entry that didn't look like a URL, such as a Google Search suggestion. For example, a match might have the URL of a Google Search result page, but it might appear to the user as "Search Google for ...". These are different from typed navigations because the user didn't type or see the destination URL. They're also related to keyword navigations.
*   `"auto_toplevel"` The page was specified in the command line or is the start page.
*   `"form_submit"` The user arrived at this page by filling out values in a form and submitting the form. Not all form submissions use this transition type.
*   `"reload"` The user reloaded the page, either by clicking the reload button or by pressing Enter in the address bar. Session restore and Reopen closed tab also use this transition type.
*   `"keyword"` The URL for this page was generated from a replaceable keyword other than the default search provider.
*   `"keyword_generated"` Corresponds to a visit generated for a keyword.

### UrlDetails

Chrome 88+

#### Properties

*   `url`

    string

    The URL for the operation. It must be in the format as returned from a call to `history.search()`.

### VisitItem

An object encapsulating one visit to a URL.

#### Properties

*   `id`

    string

    The unique identifier for the corresponding `history.HistoryItem`.
*   `isLocal`

    boolean

    Chrome 115+

    True if the visit originated on this device. False if it was synced from a different device.
*   `referringVisitId`

    string

    The visit ID of the referrer.
*   `transition`

    `TransitionType`

    The transition type for this visit from its referrer.
*   `visitId`

    string

    The unique identifier for this visit.
*   `visitTime`

    number optional

    When this visit occurred, represented in milliseconds since the epoch.

## Methods

### addUrl()

Promise

```javascript
chrome.history.addUrl(
  details: UrlDetails,
  callback?: function,
)
```

Adds a URL to the history at the current time with a transition type of `"link"`.

#### Parameters

*   `details`

    `UrlDetails`
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### deleteAll()

Promise

```javascript
chrome.history.deleteAll(callback?: function)
```

Deletes all items from the history.

#### Parameters

*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### deleteRange()

Promise

```javascript
chrome.history.deleteRange(
  range: object,
  callback?: function,
)
```

Removes all items within the specified date range from the history. Pages will not be removed from the history unless all visits fall within the range.

#### Parameters

*   `range`

    object

    *   `endTime`

        number

        Items added to history before this date, represented in milliseconds since the epoch.
    *   `startTime`

        number

        Items added to history after this date, represented in milliseconds since the epoch.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### deleteUrl()

Promise

```javascript
chrome.history.deleteUrl(
  details: UrlDetails,
  callback?: function,
)
```

Removes all occurrences of the given URL from the history.

#### Parameters

*   `details`

    `UrlDetails`
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getVisits()

Promise

```javascript
chrome.history.getVisits(
  details: UrlDetails,
  callback?: function,
)
```

Retrieves information about visits to a URL.

#### Parameters

*   `details`

    `UrlDetails`
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (results: VisitItem[]) => void
    ```

    *   `results`

        `VisitItem[]`

#### Returns

*   `Promise<VisitItem[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### search()

Promise

```javascript
chrome.history.search(
  query: object,
  callback?: function,
)
```

Searches the history for the last visit time of each page matching the query.

#### Parameters

*   `query`

    object

    *   `endTime`

        number optional

        Limit results to those visited before this date, represented in milliseconds since the epoch.
    *   `maxResults`

        number optional

        The maximum number of results to retrieve. Defaults to 100.
    *   `startTime`

        number optional

        Limit results to those visited after this date, represented in milliseconds since the epoch. If property is not specified, it will default to 24 hours.
    *   `text`

        string

        A free-text query to the history service. Leave this empty to retrieve all pages.
*   `callback`

    function optional

    The callback parameter looks like:

    ```javascript
    (results: HistoryItem[]) => void
    ```

    *   `results`

        `HistoryItem[]`

#### Returns

*   `Promise<HistoryItem[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onVisited

```javascript
chrome.history.onVisited.addListener(callback: function)
```

Fired when a URL is visited, providing the `HistoryItem` data for that URL. This event fires before the page has loaded.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (result: HistoryItem) => void
    ```

    *   `result`

        `HistoryItem`

### onVisitRemoved

```javascript
chrome.history.onVisitRemoved.addListener(callback: function)
```

Fired when one or more URLs are removed from history. When all visits have been removed the URL is purged from history.

#### Parameters

*   `callback`

    function

    The callback parameter looks like:

    ```javascript
    (removed: object) => void
    ```

    *   `removed`

        object

        *   `allHistory`

            boolean

            True if all history was removed. If true, then `urls` will be empty.
        *   `urls`

            string[] optional

===

---
title: chrome.i18n
url: https://developer.chrome.com/docs/extensions/reference/api/i18n
---

# chrome.i18n

## Description

Use the `chrome.i18n` infrastructure to implement internationalization across your whole app or extension.

## Manifest

If an extension has a `/_locales` directory, the manifest must define `"default_locale"`.

## Concepts and usage

You need to put all of its user-visible strings into a file named `messages.json`. Each time you add a new locale, you add a messages file under a directory named `/_locales/_localeCode_`, where `localeCode` is a code such as `en` for English.

Here's the file hierarchy for an internationalized extension that supports English (`en`), Spanish (`es`), and Korean (`ko`):

### Support multiple languages

Say you have an extension with the files shown in the following figure:

To internationalize this extension, you name each user-visible string and put it into a messages file. The extension's manifest, CSS files, and JavaScript code use each string's name to get its localized version.

Here's what the extension looks like when it's internationalized (note that it still has only English strings):

Some notes about internationalizing:

*   You can use any of the supported locales. If you use an unsupported locale, Google Chrome ignores it.
*   In `manifest.json` and CSS files, refer to a string named `messagename` like this:

    ```
    __MSG_messagename__
    ```
*   In your extension or app's JavaScript code, refer to a string named `messagename` like this:

    ```
    chrome.i18n.getMessage("messagename")
    ```
*   In each call to `getMessage()`, you can supply up to 9 strings to be included in the message. See Examples: `getMessage` for details.
*   Some messages, such as `@@bidi_dir` and `@@ui_locale`, are provided by the internationalization system. See the Predefined messages section for a full list of predefined message names.
*   In `messages.json`, each user-visible string has a name, a `"message"` item, and an optional `"description"` item. The name is a key such as `"extName"` or `"search_string"` that identifies the string. The `"message"` specifies the value of the string in this locale. The optional `"description"` provides help to translators, who might not be able to see how the string is used in your extension. For example:

    ```json
    { "search_string": { "message": "hello%20world", "description": "The string we search for. Put %20 between words that go together." }, ... }
    ```

For more information, see Formats: Locale-Specific Messages.

Once an extension is internationalized, translating it is straightforward. You copy `messages.json`, translate it, and put the copy into a new directory under `/_locales`. For example, to support Spanish, just put a translated copy of `messages.json` under `/_locales/es`. The following figure shows the previous extension with a new Spanish translation.

### Predefined messages

The internationalization system provides a few predefined messages to help you localize. These include `@@ui_locale`, so you can detect the current UI locale, and a few `@@bidi_...` messages that let you detect the text direction. The latter messages have similar names to constants in the gadgets BIDI (bi-directional) API.

The special message `@@extension_id` can be used in the CSS and JavaScript files, whether or not the extension or app is localized. This message doesn't work in manifest files.

The following table describes each predefined message.

| Message name        | Description                                                                                                                                                              |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `@@extension_id`    | The extension or app ID; you might use this string to construct URLs for resources inside the extension. Even unlocalized extensions can use this message. Note: You can't use this message in a manifest file. |
| `@@ui_locale`       | The current locale; you might use this string to construct locale-specific URLs.                                                                                         |
| `@@bidi_dir`        | The text direction for the current locale, either `"ltr"` for left-to-right languages such as English or `"rtl"` for right-to-left languages such as Arabic.                 |
| `@@bidi_reversed_dir` | If the `@@bidi_dir` is `"ltr"`, then this is `"rtl"`; otherwise, it's `"ltr"`.                                                                                             |
| `@@bidi_start_edge` | If the `@@bidi_dir` is `"ltr"`, then this is `"left"`; otherwise, it's `"right"`.                                                                                           |
| `@@bidi_end_edge`   | If the `@@bidi_dir` is `"ltr"`, then this is `"right"`; otherwise, it's `"left"`.                                                                                            |

Here's an example of using `@@extension_id` in a CSS file to construct a URL:

```css
body { background-image:url('chrome-extension://__MSG_@@extension_id__/background.png'); }
```

If the extension ID is `abcdefghijklmnopqrstuvwxyzabcdef`, then the bold line in the previous code snippet becomes:

```css
background-image:url('chrome-extension://abcdefghijklmnopqrstuvwxyzabcdef/background.png');
```

Here's an example of using `@@bidi_*` messages in a CSS file:

```css
body { direction: __MSG_@@bidi_dir__; } div#header { margin-bottom: 1.05em; overflow: hidden; padding-bottom: 1.5em; padding-__MSG_@@bidi_start_edge__: 0; padding-__MSG_@@bidi_end_edge__: 1.5em; position: relative; }
```

For left-to-right languages such as English, the bold lines become:

```css
dir: ltr; padding-left: 0; padding-right: 1.5em;
```

### Locales

You can choose from many locales, including some (such as `en`) that let a single translation support multiple variations of a language (such as `en_GB` and `en_US`).

You can localize your extension to any locale that is supported by the Chrome Web Store. If your locale is not listed here, choose the closest alternative. For example, if the default locale of your extension is `"de_CH"`, choose `"de"` in the Chrome Web Store.

| Locale code | Language (region)                   |
| ----------- | ----------------------------------- |
| `ar`        | Arabic                              |
| `am`        | Amharic                             |
| `bg`        | Bulgarian                           |
| `bn`        | Bengali                             |
| `ca`        | Catalan                             |
| `cs`        | Czech                               |
| `da`        | Danish                              |
| `de`        | German                              |
| `el`        | Greek                               |
| `en`        | English                             |
| `en_AU`     | English (Australia)                 |
| `en_GB`     | English (Great Britain)             |
| `en_US`     | English (USA)                       |
| `es`        | Spanish                             |
| `es_419`    | Spanish (Latin America and Caribbean) |
| `et`        | Estonian                            |
| `fa`        | Persian                             |
| `fi`        | Finnish                             |
| `fil`       | Filipino                            |
| `fr`        | French                              |
| `gu`        | Gujarati                            |
| `he`        | Hebrew                              |
| `hi`        | Hindi                               |
| `hr`        | Croatian                            |
| `hu`        | Hungarian                           |
| `id`        | Indonesian                          |
| `it`        | Italian                             |
| `ja`        | Japanese                            |
| `kn`        | Kannada                             |
| `ko`        | Korean                              |
| `lt`        | Lithuanian                          |
| `lv`        | Latvian                             |
| `ml`        | Malayalam                           |
| `mr`        | Marathi                             |
| `ms`        | Malay                               |
| `nl`        | Dutch                               |
| `no`        | Norwegian                           |
| `pl`        | Polish                              |
| `pt_BR`     | Portuguese (Brazil)                 |
| `pt_PT`     | Portuguese (Portugal)               |
| `ro`        | Romanian                            |
| `ru`        | Russian                             |
| `sk`        | Slovak                              |
| `sl`        | Slovenian                           |
| `sr`        | Serbian                             |
| `sv`        | Swedish                             |
| `sw`        | Swahili                             |
| `ta`        | Tamil                               |
| `te`        | Telugu                              |
| `th`        | Thai                                |
| `tr`        | Turkish                             |
| `uk`        | Ukrainian                           |
| `vi`        | Vietnamese                          |
| `zh_CN`     | Chinese (China)                     |
| `zh_TW`     | Chinese (Taiwan)                    |

### Search for messages

You don't have to define every string for every supported locale. As long as the default locale's `messages.json` file has a value for every string, your extension or app will run no matter how sparse a translation is. Here's how the extension system searches for a message:

1.  Search the messages file (if any) for the user's preferred locale. For example, when Google Chrome's locale is set to British English (`en_GB`), the system first looks for the message in `/_locales/en_GB/messages.json`. If that file exists and the message is there, the system looks no further.
2.  If the user's preferred locale has a region (that is, the locale has an underscore: `_`), search the locale without that region. For example, if the `en_GB` messages file doesn't exist or doesn't contain the message, the system looks in the `en` messages file. If that file exists and the message is there, the system looks no further.
3.  Search the messages file for the default locale. For example, if the extension's `"default_locale"` is set to `"es"`, and neither `/_locales/en_GB/messages.json` nor `/_locales/en/messages.json` contains the message, the extension uses the message from `/_locales/es/messages.json`.

In the following figure, the message named `"colores"` is in all three locales that the extension supports, but `"extName"` is in only two of the locales. Wherever a user running Google Chrome in US English sees the label "Colors", a user of British English sees "Colours". Both US English and British English users see the extension name "Hello World". Because the default language is Spanish, users running Google Chrome in any non-English language see the label "Colores" and the extension name "Hola mundo".

### Set your browser's locale

To test translations, you might want to set your browser's locale. This section tells you how to set the locale in Windows, Mac OS, Linux, and ChromeOS.

#### Windows

You can change the locale using either a locale-specific shortcut or the Google Chrome UI. The shortcut approach is quicker, once you've set it up, and it lets you use several languages at once.

##### Use a locale-specific shortcut

To create and use a shortcut that launches Google Chrome with a particular locale:

1.  Make a copy of the Google Chrome shortcut that's already on your desktop.
2.  Rename the new shortcut to match the new locale.
3.  Change the shortcut's properties so that the Target field specifies the `--lang` and `--user-data-dir` flags. The target should look something like this:

    ```
    path_to_chrome.exe --lang=locale --user-data-dir=c:\locale_profile_dir
    ```
4.  Launch Google Chrome by double-clicking the shortcut.

For example, to create a shortcut that launches Google Chrome in Spanish (`es`), you might create a shortcut named `chrome-es` that has the following target:

```
path_to_chrome.exe --lang=es --user-data-dir=c:\chrome-profile-es
```

You can create as many shortcuts as you like, making it straightforward to test in multiple languages. For example:

```
path_to_chrome.exe --lang=en --user-data-dir=c:\chrome-profile-en path_to_chrome.exe --lang=en_GB --user-data-dir=c:\chrome-profile-en_GB path_to_chrome.exe --lang=ko --user-data-dir=c:\chrome-profile-ko
```

Note: Specifying `--user-data-dir` is optional but handy. Having one data directory per locale lets you run the browser in several languages at the same time. A disadvantage is that because the locales' data isn't shared, you have to install your extension multiple times鈥攐nce per locale, which can be challenging when you don't speak the language. For more information, see Creating and Using Profiles.

##### Use the UI

Here's how to change the locale using the UI on Google Chrome for Windows:

1.  App icon > Options
2.  Choose the Under the Hood tab
3.  Scroll to Web Content
4.  Click Change font and language settings
5.  Choose the Languages tab
6.  Use the drop down to set the Google Chrome language
7.  Restart Chrome

#### Mac OS

To change the locale on Mac, you use the system preferences.

1.  From the Apple menu, choose System Preferences
2.  Under the Personal section, choose International
3.  Choose your language and location
4.  Restart Chrome

#### Linux

To change the locale on Linux, first quit Google Chrome. Then, all in one line, set the `LANGUAGE` environment variable and launch Google Chrome. For example:

```
LANGUAGE=es ./chrome
```

#### ChromeOS

To change the locale on ChromeOS:

1.  From the system tray, choose Settings.
2.  Under the Languages and input section, choose the Language drop-down.
3.  If your language is not listed, click Add languages and add it.
4.  Once added, click the 3-dot More actions menu item next to your language and choose Display ChromeOS in this language.
5.  Click the Restart button that appears next to the set language to restart ChromeOS.

## Examples

You can find examples of internationalization in the `examples/api/i18n` directory. For a complete example, see `examples/extensions/news`. For other examples and for help in viewing the source code, see Samples.

### getMessage()

The following code gets a localized message from the browser and displays it as a string. It replaces two placeholders within the message with the strings `"string1"` and `"string2"`.

```javascript
function getMessage() { var message = chrome.i18n.getMessage("click_here", ["string1", "string2"]); document.getElementById("languageSpan").innerHTML = message; }
```

Here's how you'd supply and use a single string:

```javascript
// In JavaScript code status.innerText = chrome.i18n.getMessage("error", errorDetails);
```

```json
"error": { "message": "Error: $details$", "description": "Generic error template. Expects error parameter to be passed in.", "placeholders": { "details": { "content": "$1", "example": "Failed to fetch RSS feed." } } }
```

For more information about placeholders, see the Locale-Specific Messages page. For details on calling `getMessage()`, see the API reference.

### getAcceptLanguages()

The following code gets accept-languages from the browser and displays them as a string by separating each accept-language with `,`.

```javascript
function getAcceptLanguages() { chrome.i18n.getAcceptLanguages(function(languageList) { var languages = languageList.join(","); document.getElementById("languageSpan").innerHTML = languages; }) }
```

For details on calling `getAcceptLanguages()`, see the API reference.

### detectLanguage()

The following code detects up to 3 languages from the given string and displays the result as strings separated by new lines.

```javascript
function detectLanguage(inputText) { chrome.i18n.detectLanguage(inputText, function(result) { var outputLang = "Detected Language: "; var outputPercent = "Language Percentage: "; for(i = 0; i < result.languages.length; i++) { outputLang += result.languages[i].language + " "; outputPercent +=result.languages[i].percentage + " "; } document.getElementById("languageSpan").innerHTML = outputLang + "\n" + outputPercent + "\nReliable: " + result.isReliable; }); }
```

For more details on calling `detectLanguage(inputText)`, see the API reference.

## Types

### LanguageCode

Chrome 47+

An ISO language code such as `en` or `fr`. For a complete list of languages supported by this method, see `kLanguageInfoTable`. For an unknown language, `und` will be returned, which means that `[percentage]` of the text is unknown to CLD

#### Type

`string`

## Methods

### detectLanguage()

Promise Chrome 47+

```
chrome.i18n.detectLanguage( text: string, callback?: function, )
```

Detects the language of the provided text using CLD.

#### Parameters

*   `text`

    `string`

    User input string to be translated.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (result: object) => void
    ```

    *   `result`

        `object`

        `LanguageDetectionResult` object that holds detected langugae reliability and array of `DetectedLanguage`

        *   `isReliable`

            `boolean`

            CLD detected language reliability
        *   `languages`

            `object[]`

            array of `detectedLanguage`

            *   `language`

                `string`
            *   `percentage`

                `number`

                The percentage of the detected language

#### Returns

*   `Promise<object>`

    Chrome 99+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAcceptLanguages()

Promise

```
chrome.i18n.getAcceptLanguages( callback?: function, )
```

Gets the accept-languages of the browser. This is different from the locale used by the browser; to get the locale, use `i18n.getUILanguage`.

#### Parameters

*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (languages: string[]) => void
    ```

    *   `languages`

        `string[]`

        Array of `LanguageCode`

#### Returns

*   `Promise<LanguageCode[]>`

    Chrome 99+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getMessage()

```
chrome.i18n.getMessage( messageName: string, substitutions?: any, options?: object, )
```

Gets the localized string for the specified message. If the message is missing, this method returns an empty string (`''`). If the format of the `getMessage()` call is wrong 鈥?for example, `messageName` is not a string or the `substitutions` array has more than 9 elements 鈥?this method returns `undefined`.

#### Parameters

*   `messageName`

    `string`

    The name of the message, as specified in the `messages.json` file.
*   `substitutions`

    `any` optional

    Up to 9 substitution strings, if the message requires any.
*   `options`

    `object` optional

    Chrome 79+

    *   `escapeLt`

        `boolean` optional

        Escape `<` in translation to `&lt;`. This applies only to the message itself, not to the placeholders. Developers might want to use this if the translation is used in an HTML context. Closure Templates used with Closure Compiler generate this automatically.

#### Returns

*   `string`

    Message localized for current locale.

### getUILanguage()

```
chrome.i18n.getUILanguage()
```

Gets the browser UI language of the browser. This is different from `i18n.getAcceptLanguages` which returns the preferred user languages.

#### Returns

*   `string`

    The browser UI language code such as `en-US` or `fr-FR`.

===

---
title: chrome.identity
url: https://developer.chrome.com/docs/extensions/reference/api/identity
---

# chrome.identity

## Description

Use the `chrome.identity` API to get OAuth2 access tokens.

## Permissions

`identity`

## Types

### AccountInfo

#### Properties

*   `id`

    `string`

    A unique identifier for the account. This ID will not change for the lifetime of the account.

### AccountStatus

Chrome 84+

#### Enum

`"SYNC"` Specifies that Sync is enabled for the primary account.

`"ANY"` Specifies the existence of a primary account, if any.

### GetAuthTokenResult

Chrome 105+

#### Properties

*   `grantedScopes`

    `string[]` optional

    A list of OAuth2 scopes granted to the extension.
*   `token`

    `string` optional

    The specific token associated with the request.

### InvalidTokenDetails

#### Properties

*   `token`

    `string`

    The specific token that should be removed from the cache.

### ProfileDetails

Chrome 84+

#### Properties

*   `accountStatus`

    `AccountStatus` optional

    A status of the primary account signed into a profile whose `ProfileUserInfo` should be returned. Defaults to `SYNC` account status.

### ProfileUserInfo

#### Properties

*   `email`

    `string`

    An email address for the user account signed into the current profile. Empty if the user is not signed in or the `identity.email` manifest permission is not specified.
*   `id`

    `string`

    A unique identifier for the account. This ID will not change for the lifetime of the account. Empty if the user is not signed in or (in M41+) the `identity.email` manifest permission is not specified.

### TokenDetails

#### Properties

*   `account`

    `AccountInfo` optional

    The account ID whose token should be returned. If not specified, the function will use an account from the Chrome profile: the Sync account if there is one, or otherwise the first Google web account.
*   `enableGranularPermissions`

    `boolean` optional

    Chrome 87+

    The `enableGranularPermissions` flag allows extensions to opt-in early to the granular permissions consent screen, in which requested permissions are granted or denied individually.
*   `interactive`

    `boolean` optional

    Fetching a token may require the user to sign-in to Chrome, or approve the application's requested scopes. If the `interactive` flag is true, `getAuthToken` will prompt the user as necessary. When the flag is false or omitted, `getAuthToken` will return failure any time a prompt would be required.
*   `scopes`

    `string[]` optional

    A list of OAuth2 scopes to request.

    When the `scopes` field is present, it overrides the list of scopes specified in `manifest.json`.

### WebAuthFlowDetails

#### Properties

*   `abortOnLoadForNonInteractive`

    `boolean` optional

    Chrome 113+

    Whether to terminate `launchWebAuthFlow` for non-interactive requests after the page loads. This parameter does not affect interactive flows.

    When set to `true` (default) the flow will terminate immediately after the page loads. When set to `false`, the flow will only terminate after the `timeoutMsForNonInteractive` passes. This is useful for identity providers that use JavaScript to perform redirections after the page loads.
*   `interactive`

    `boolean` optional

    Whether to launch auth flow in interactive mode.

    Since some auth flows may immediately redirect to a result URL, `launchWebAuthFlow` hides its web view until the first navigation either redirects to the final URL, or finishes loading a page meant to be displayed.

    If the `interactive` flag is true, the window will be displayed when a page load completes. If the flag is false or omitted, `launchWebAuthFlow` will return with an error if the initial navigation does not complete the flow.

    For flows that use JavaScript for redirection, `abortOnLoadForNonInteractive` can be set to `false` in combination with setting `timeoutMsForNonInteractive` to give the page a chance to perform any redirects.
*   `timeoutMsForNonInteractive`

    `number` optional

    Chrome 113+

    The maximum amount of time, in miliseconds, `launchWebAuthFlow` is allowed to run in non-interactive mode in total. Only has an effect if `interactive` is false.
*   `url`

    `string`

    The URL that initiates the auth flow.

## Methods

### clearAllCachedAuthTokens()

Promise Chrome 87+

```
chrome.identity.clearAllCachedAuthTokens( callback?: function, )
```

Resets the state of the Identity API:

*   Removes all OAuth2 access tokens from the token cache
*   Removes user's account preferences
*   De-authorizes the user from all auth flows

#### Parameters

*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 106+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAccounts()

Promise Dev channel

```
chrome.identity.getAccounts( callback?: function, )
```

Retrieves a list of `AccountInfo` objects describing the accounts present on the profile.

`getAccounts` is only supported on dev channel.

#### Parameters

*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (accounts: AccountInfo[]) => void
    ```

    *   `accounts`

        `AccountInfo[]`

#### Returns

*   `Promise<AccountInfo[]>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAuthToken()

Promise

```
chrome.identity.getAuthToken( details?: TokenDetails, callback?: function, )
```

Gets an OAuth2 access token using the client ID and scopes specified in the `oauth2` section of `manifest.json`.

The Identity API caches access tokens in memory, so it's ok to call `getAuthToken` non-interactively any time a token is required. The token cache automatically handles expiration.

For a good user experience it is important interactive token requests are initiated by UI in your app explaining what the authorization is for. Failing to do this will cause your users to get authorization requests, or Chrome sign in screens if they are not signed in, with with no context. In particular, do not use `getAuthToken` interactively when your app is first launched.

Note: When called with a callback, instead of returning an object this function will return the two properties as separate arguments passed to the callback.

#### Parameters

*   `details`

    `TokenDetails` optional

    Token options.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (result: GetAuthTokenResult) => void
    ```

    *   `result`

        `GetAuthTokenResult`

        Chrome 105+

#### Returns

*   `Promise<GetAuthTokenResult>`

    Chrome 105+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getProfileUserInfo()

Promise

```
chrome.identity.getProfileUserInfo( details?: ProfileDetails, callback?: function, )
```

Retrieves email address and obfuscated gaia id of the user signed into a profile.

Requires the `identity.email` manifest permission. Otherwise, returns an empty result.

This API is different from `identity.getAccounts` in two ways. The information returned is available offline, and it only applies to the primary account for the profile.

#### Parameters

*   `details`

    `ProfileDetails` optional

    Chrome 84+

    Profile options.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (userInfo: ProfileUserInfo) => void
    ```

    *   `userInfo`

        `ProfileUserInfo`

#### Returns

*   `Promise<ProfileUserInfo>`

    Chrome 106+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getRedirectURL()

```
chrome.identity.getRedirectURL( path?: string, )
```

Generates a redirect URL to be used in `launchWebAuthFlow`.

The generated URLs match the pattern `https://<app-id>.chromiumapp.org/*`.

#### Parameters

*   `path`

    `string` optional

    The path appended to the end of the generated URL.

#### Returns

*   `string`

### launchWebAuthFlow()

Promise

```
chrome.identity.launchWebAuthFlow( details: WebAuthFlowDetails, callback?: function, )
```

Starts an auth flow at the specified URL.

This method enables auth flows with non-Google identity providers by launching a web view and navigating it to the first URL in the provider's auth flow. When the provider redirects to a URL matching the pattern `https://<app-id>.chromiumapp.org/*`, the window will close, and the final redirect URL will be passed to the callback function.

For a good user experience it is important interactive auth flows are initiated by UI in your app explaining what the authorization is for. Failing to do this will cause your users to get authorization requests with no context. In particular, do not launch an interactive auth flow when your app is first launched.

#### Parameters

*   `details`

    `WebAuthFlowDetails`

    WebAuth flow options.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (responseUrl?: string) => void
    ```

    *   `responseUrl`

        `string` optional

#### Returns

*   `Promise<string | undefined>`

    Chrome 106+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeCachedAuthToken()

Promise

```
chrome.identity.removeCachedAuthToken( details: InvalidTokenDetails, callback?: function, )
```

Removes an OAuth2 access token from the Identity API's token cache.

If an access token is discovered to be invalid, it should be passed to `removeCachedAuthToken` to remove it from the cache. The app may then retrieve a fresh token with `getAuthToken`.

#### Parameters

*   `details`

    `InvalidTokenDetails`

    Token information.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 106+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onSignInChanged

```
chrome.identity.onSignInChanged.addListener( callback: function, )
```

Fired when signin state changes for an account on the user's profile.

#### Parameters

*   `callback`

    `function`

    The `callback` parameter looks like:

    ```
    (account: AccountInfo, signedIn: boolean) => void
    ```

    *   `account`

        `AccountInfo`
    *   `signedIn`

        `boolean`

===

---
title: chrome.idle
url: https://developer.chrome.com/docs/extensions/reference/api/idle
---

# chrome.idle

## Description

Use the `chrome.idle` API to detect when the machine's idle state changes.

## Permissions

`idle`

You must declare the `"idle"` permission in your extension's manifest to use the idle API. For example:

```json
{ "name": "My extension", ... "permissions": [ "idle" ], ... }
```

## Types

### IdleState

Chrome 44+

#### Enum

`"active"`

`"idle"`

`"locked"`

## Methods

### getAutoLockDelay()

Promise Chrome 73+ ChromeOS only

```
chrome.idle.getAutoLockDelay( callback?: function, )
```

Gets the time, in seconds, it takes until the screen is locked automatically while idle. Returns a zero duration if the screen is never locked automatically. Currently supported on Chrome OS only.

#### Parameters

*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (delay: number) => void
    ```

    *   `delay`

        `number`

        Time, in seconds, until the screen is locked automatically while idle. This is zero if the screen never locks automatically.

#### Returns

*   `Promise<number>`

    Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### queryState()

Promise

```
chrome.idle.queryState( detectionIntervalInSeconds: number, callback?: function, )
```

Returns `"locked"` if the system is locked, `"idle"` if the user has not generated any input for a specified number of seconds, or `"active"` otherwise.

#### Parameters

*   `detectionIntervalInSeconds`

    `number`

    The system is considered idle if `detectionIntervalInSeconds` seconds have elapsed since the last user input detected.
*   `callback`

    `function` optional

    The `callback` parameter looks like:

    ```
    (newState: IdleState) => void
    ```

    *   `newState`

        `IdleState`

#### Returns

*   `Promise<IdleState>`

    Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setDetectionInterval()

```
chrome.idle.setDetectionInterval( intervalInSeconds: number, )
```

Sets the interval, in seconds, used to determine when the system is in an idle state for `onStateChanged` events. The default interval is 60 seconds.

#### Parameters

*   `intervalInSeconds`

    `number`

    Threshold, in seconds, used to determine when the system is in an idle state.

## Events

### onStateChanged

```
chrome.idle.onStateChanged.addListener( callback: function, )
```

Fired when the system changes to an active, idle or locked state. The event fires with `"locked"` if the screen is locked or the screensaver activates, `"idle"` if the system is unlocked and the user has not generated any input for a specified number of seconds, and `"active"` when the user generates input on an idle system.

#### Parameters

*   `callback`

    `function`

    The `callback` parameter looks like:

    ```
    (newState: IdleState) => void
    ```

    *   `newState`

        `IdleState`

===

---
title: chrome.input.ime
url: https://developer.chrome.com/docs/extensions/reference/api/input/ime
---

# chrome.input.ime

Important: This API works only on ChromeOS.

## Description

Use the `chrome.input.ime` API to implement a custom IME for Chrome OS. This allows your extension to handle keystrokes, set the composition, and manage the candidate window.

## Permissions

`input`

You must declare the "input" permission in the extension manifest to use the `input.ime` API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "input"
  ],
  ...
}
```

## Availability

ChromeOS only

## Examples

The following code creates an IME that converts typed letters to upper case.

```javascript
var context_id = -1;
chrome.input.ime.onFocus.addListener(function(context) {
  context_id = context.contextID;
});
chrome.input.ime.onKeyEvent.addListener(
  function(engineID, keyData) {
    if (keyData.type == "keydown" && keyData.key.match(/^[a-z]$/)) {
      chrome.input.ime.commitText({"contextID": context_id,
                                  "text": keyData.key.toUpperCase()});
      return true;
    } else {
      return false;
    }
  }
);
```

## Types

### AssistiveWindowButton

Chrome 85+

ID of buttons in assistive window.

#### Enum

"undo"

"addToDictionary"

### AssistiveWindowProperties

Chrome 85+

Properties of the assistive window.

#### Properties

*   `announceString`
    string optional
    Strings for ChromeVox to announce.
*   `type`
    "undo"
*   `visible`
    boolean
    Sets `true` to show AssistiveWindow, sets `false` to hide.

### AssistiveWindowType

Chrome 85+

Type of assistive window.

#### Value

"undo"

### AutoCapitalizeType

Chrome 69+

The auto-capitalize type of the text field.

#### Enum

"characters"

"words"

"sentences"

### InputContext

Describes an input Context

#### Properties

*   `autoCapitalize`
    `AutoCapitalizeType`
    Chrome 69+
    The auto-capitalize type of the text field.
*   `autoComplete`
    boolean
    Whether the text field wants auto-complete.
*   `autoCorrect`
    boolean
    Whether the text field wants auto-correct.
*   `contextID`
    number
    This is used to specify targets of text field operations. This ID becomes invalid as soon as `onBlur` is called.
*   `shouldDoLearning`
    boolean
    Chrome 68+
    Whether text entered into the text field should be used to improve typing suggestions for the user.
*   `spellCheck`
    boolean
    Whether the text field wants spell-check.
*   `type`
    `InputContextType`
    Type of value this text field edits, (Text, Number, URL, etc)

### InputContextType

Chrome 44+

Type of value this text field edits, (Text, Number, URL, etc)

#### Enum

"text"

"search"

"tel"

"url"

"email"

"number"

"password"

"null"

### KeyboardEvent

See http://www.w3.org/TR/DOM-Level-3-Events/#events-KeyboardEvent

#### Properties

*   `altKey`
    boolean optional
    Whether or not the ALT key is pressed.
*   `altgrKey`
    boolean optional
    Chrome 79+
    Whether or not the ALTGR key is pressed.
*   `capsLock`
    boolean optional
    Whether or not the CAPS_LOCK is enabled.
*   `code`
    string
    Value of the physical key being pressed. The value is not affected by current keyboard layout or modifier state.
*   `ctrlKey`
    boolean optional
    Whether or not the CTRL key is pressed.
*   `extensionId`
    string optional
    The extension ID of the sender of this keyevent.
*   `key`
    string
    Value of the key being pressed
*   `keyCode`
    number optional
    The deprecated HTML keyCode, which is system- and implementation-dependent numerical code signifying the unmodified identifier associated with the key pressed.
*   `requestId`
    string optional
    (Deprecated) The ID of the request. Use the `requestId` param from the `onKeyEvent` event instead.
*   `shiftKey`
    boolean optional
    Whether or not the SHIFT key is pressed.
*   `type`
    `KeyboardEventType`
    One of `keyup` or `keydown`.

### KeyboardEventType

Chrome 44+

#### Enum

"keyup"

"keydown"

### MenuItem

A menu item used by an input method to interact with the user from the language menu.

#### Properties

*   `checked`
    boolean optional
    Indicates this item should be drawn with a check.
*   `enabled`
    boolean optional
    Indicates this item is enabled.
*   `id`
    string
    String that will be passed to callbacks referencing this `MenuItem`.
*   `label`
    string optional
    Text displayed in the menu for this item.
*   `style`
    `MenuItemStyle` optional
    The type of menu item.
*   `visible`
    boolean optional
    Indicates this item is visible.

### MenuItemStyle

Chrome 44+

The type of menu item. Radio buttons between separators are considered grouped.

#### Enum

"check"

"radio"

"separator"

### MenuParameters

Chrome 88+

#### Properties

*   `engineID`
    string
    ID of the engine to use.
*   `items`
    `MenuItem`[]
    `MenuItems` to add or update. They will be added in the order they exist in the array.

### MouseButton

Chrome 44+

Which mouse buttons was clicked.

#### Enum

"left"

"middle"

"right"

### ScreenType

Chrome 44+

The screen type under which the IME is activated.

#### Enum

"normal"

"login"

"lock"

"secondary-login"

### UnderlineStyle

Chrome 44+

The type of the underline to modify this segment.

#### Enum

"underline"

"doubleUnderline"

"noUnderline"

### WindowPosition

Chrome 44+

Where to display the candidate window. If set to 'cursor', the window follows the cursor. If set to 'composition', the window is locked to the beginning of the composition.

#### Enum

"cursor"

"composition"

## Methods

### clearComposition()

Promise

```
chrome.input.ime.clearComposition(
  parameters: object,
  callback?: function,
)
```

Clear the current composition. If this extension does not own the active IME, this fails.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context where the composition will be cleared
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### commitText()

Promise

```
chrome.input.ime.commitText(
  parameters: object,
  callback?: function,
)
```

Commits the provided text to the current input.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context where the text will be committed
    *   `text`
        string
        The text to commit
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### deleteSurroundingText()

Promise

```
chrome.input.ime.deleteSurroundingText(
  parameters: object,
  callback?: function,
)
```

Deletes the text around the caret.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context where the surrounding text will be deleted.
    *   `engineID`
        string
        ID of the engine receiving the event.
    *   `length`
        number
        The number of characters to be deleted
    *   `offset`
        number
        The offset from the caret position where deletion will start. This value can be negative.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### hideInputView()

```
chrome.input.ime.hideInputView()
```

Hides the input view window, which is popped up automatically by system. If the input view window is already hidden, this function will do nothing.

### keyEventHandled()

```
chrome.input.ime.keyEventHandled(
  requestId: string,
  response: boolean,
)
```

Indicates that the key event received by `onKeyEvent` is handled. This should only be called if the `onKeyEvent` listener is asynchronous.

#### Parameters

*   `requestId`
    string
    Request id of the event that was handled. This should come from `keyEvent.requestId`
*   `response`
    boolean
    `True` if the keystroke was handled, `false` if not

### sendKeyEvents()

Promise

```
chrome.input.ime.sendKeyEvents(
  parameters: object,
  callback?: function,
)
```

Sends the key events. This function is expected to be used by virtual keyboards. When key(s) on a virtual keyboard is pressed by a user, this function is used to propagate that event to the system.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context where the key events will be sent, or zero to send key events to non-input field.
    *   `keyData`
        `KeyboardEvent`[]
        Data on the key event.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setAssistiveWindowButtonHighlighted()

Promise Chrome 86+

```
chrome.input.ime.setAssistiveWindowButtonHighlighted(
  parameters: object,
  callback?: function,
)
```

Highlights/Unhighlights a button in an assistive window.

#### Parameters

*   `parameters`
    object
    *   `announceString`
        string optional
        The text for the screenreader to announce.
    *   `buttonID`
        `AssistiveWindowButton`
        The ID of the button
    *   `contextID`
        number
        ID of the context owning the assistive window.
    *   `highlighted`
        boolean
        Whether the button should be highlighted.
    *   `windowType`
        "undo"
        The window type the button belongs to.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setAssistiveWindowProperties()

Promise Chrome 85+

```
chrome.input.ime.setAssistiveWindowProperties(
  parameters: object,
  callback?: function,
)
```

Shows/Hides an assistive window with the given properties.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context owning the assistive window.
    *   `properties`
        `AssistiveWindowProperties`
        Properties of the assistive window.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setCandidates()

Promise

```
chrome.input.ime.setCandidates(
  parameters: object,
  callback?: function,
)
```

Sets the current candidate list. This fails if this extension doesn't own the active IME

#### Parameters

*   `parameters`
    object
    *   `candidates`
        object[]
        List of candidates to show in the candidate window
        *   `annotation`
            string optional
            Additional text describing the candidate
        *   `candidate`
            string
            The candidate
        *   `id`
            number
            The candidate's id
        *   `label`
            string optional
            Short string displayed to next to the candidate, often the shortcut key or index
        *   `parentId`
            number optional
            The id to add these candidates under
        *   `usage`
            object optional
            The usage or detail description of word.
            *   `body`
                string
                The body string of detail description.
            *   `title`
                string
                The title string of details description.
    *   `contextID`
        number
        ID of the context that owns the candidate window.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setCandidateWindowProperties()

Promise

```
chrome.input.ime.setCandidateWindowProperties(
  parameters: object,
  callback?: function,
)
```

Sets the properties of the candidate window. This fails if the extension doesn't own the active IME

#### Parameters

*   `parameters`
    object
    *   `engineID`
        string
        ID of the engine to set properties on.
    *   `properties`
        object
        *   `auxiliaryText`
            string optional
            Text that is shown at the bottom of the candidate window.
        *   `auxiliaryTextVisible`
            boolean optional
            `True` to display the auxiliary text, `false` to hide it.
        *   `currentCandidateIndex`
            number optional
            Chrome 84+
            The index of the current chosen candidate out of total candidates.
        *   `cursorVisible`
            boolean optional
            `True` to show the cursor, `false` to hide it.
        *   `pageSize`
            number optional
            The number of candidates to display per page.
        *   `totalCandidates`
            number optional
            Chrome 84+
            The total number of candidates for the candidate window.
        *   `vertical`
            boolean optional
            `True` if the candidate window should be rendered vertical, `false` to make it horizontal.
        *   `visible`
            boolean optional
            `True` to show the Candidate window, `false` to hide it.
        *   `windowPosition`
            `WindowPosition` optional
            Where to display the candidate window.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setComposition()

Promise

```
chrome.input.ime.setComposition(
  parameters: object,
  callback?: function,
)
```

Set the current composition. If this extension does not own the active IME, this fails.

#### Parameters

*   `parameters`
    object
    *   `contextID`
        number
        ID of the context where the composition text will be set
    *   `cursor`
        number
        Position in the text of the cursor.
    *   `segments`
        object[] optional
        List of segments and their associated types.
        *   `end`
            number
            Index of the character to end this segment after.
        *   `start`
            number
            Index of the character to start this segment at
        *   `style`
            `UnderlineStyle`
            The type of the underline to modify this segment.
    *   `selectionEnd`
        number optional
        Position in the text that the selection ends at.
    *   `selectionStart`
        number optional
        Position in the text that the selection starts at.
    *   `text`
        string
        Text to set
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setCursorPosition()

Promise

```
chrome.input.ime.setCursorPosition(
  parameters: object,
  callback?: function,
)
```

Set the position of the cursor in the candidate window. This is a no-op if this extension does not own the active IME.

#### Parameters

*   `parameters`
    object
    *   `candidateID`
        number
        ID of the candidate to select.
    *   `contextID`
        number
        ID of the context that owns the candidate window.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setMenuItems()

Promise

```
chrome.input.ime.setMenuItems(
  parameters: MenuParameters,
  callback?: function,
)
```

Adds the provided menu items to the language menu when this IME is active.

#### Parameters

*   `parameters`
    `MenuParameters`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### updateMenuItems()

Promise

```
chrome.input.ime.updateMenuItems(
  parameters: MenuParameters,
  callback?: function,
)
```

Updates the state of the `MenuItems` specified

#### Parameters

*   `parameters`
    `MenuParameters`
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 111+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onActivate

```
chrome.input.ime.onActivate.addListener(
  callback: function,
)
```

This event is sent when an IME is activated. It signals that the IME will be receiving `onKeyPress` events.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string, screen: ScreenType) => void
    ```
    *   `engineID`
        string
    *   `screen`
        `ScreenType`

### onAssistiveWindowButtonClicked

Chrome 85+

```
chrome.input.ime.onAssistiveWindowButtonClicked.addListener(
  callback: function,
)
```

This event is sent when a button in an assistive window is clicked.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (details: object) => void
    ```
    *   `details`
        object
        *   `buttonID`
            `AssistiveWindowButton`
            The ID of the button clicked.
        *   `windowType`
            `AssistiveWindowType`
            The type of the assistive window.

### onBlur

```
chrome.input.ime.onBlur.addListener(
  callback: function,
)
```

This event is sent when focus leaves a text box. It is sent to all extensions that are listening to this event, and enabled by the user.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (contextID: number) => void
    ```
    *   `contextID`
        number

### onCandidateClicked

```
chrome.input.ime.onCandidateClicked.addListener(
  callback: function,
)
```

This event is sent if this extension owns the active IME.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string, candidateID: number, button: MouseButton) => void
    ```
    *   `engineID`
        string
    *   `candidateID`
        number
    *   `button`
        `MouseButton`

### onDeactivated

```
chrome.input.ime.onDeactivated.addListener(
  callback: function,
)
```

This event is sent when an IME is deactivated. It signals that the IME will no longer be receiving `onKeyPress` events.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string) => void
    ```
    *   `engineID`
        string

### onFocus

```
chrome.input.ime.onFocus.addListener(
  callback: function,
)
```

This event is sent when focus enters a text box. It is sent to all extensions that are listening to this event, and enabled by the user.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (context: InputContext) => void
    ```
    *   `context`
        `InputContext`

### onInputContextUpdate

```
chrome.input.ime.onInputContextUpdate.addListener(
  callback: function,
)
```

This event is sent when the properties of the current `InputContext` change, such as the the type. It is sent to all extensions that are listening to this event, and enabled by the user.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (context: InputContext) => void
    ```
    *   `context`
        `InputContext`

### onKeyEvent

```
chrome.input.ime.onKeyEvent.addListener(
  callback: function,
)
```

Fired when a key event is sent from the operating system. The event will be sent to the extension if this extension owns the active IME. The listener function should return `true` if the event was handled `false` if it was not. If the event will be evaluated asynchronously, this function must return undefined and the IME must later call `keyEventHandled()` with the result.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string, keyData: KeyboardEvent, requestId: string) => boolean | undefined
    ```
    *   `engineID`
        string
    *   `keyData`
        `KeyboardEvent`
    *   `requestId`
        string
    *   returns
        boolean | undefined

### onMenuItemActivated

```
chrome.input.ime.onMenuItemActivated.addListener(
  callback: function,
)
```

Called when the user selects a menu item

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string, name: string) => void
    ```
    *   `engineID`
        string
    *   `name`
        string

### onReset

```
chrome.input.ime.onReset.addListener(
  callback: function,
)
```

This event is sent when chrome terminates ongoing text input session.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string) => void
    ```
    *   `engineID`
        string

### onSurroundingTextChanged

```
chrome.input.ime.onSurroundingTextChanged.addListener(
  callback: function,
)
```

Called when the editable string around caret is changed or when the caret position is moved. The text length is limited to 100 characters for each back and forth direction.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (engineID: string, surroundingInfo: object) => void
    ```
    *   `engineID`
        string
    *   `surroundingInfo`
        object
        *   `anchor`
            number
            The beginning position of the selection. This value indicates caret position if there is no selection.
        *   `focus`
            number
            The ending position of the selection. This value indicates caret position if there is no selection.
        *   `offset`
            number
            Chrome 46+
            The offset position of text. Since text only includes a subset of text around the cursor, offset indicates the absolute position of the first character of text.
        *   `text`
            string
            The text around the cursor. This is only a subset of all text in the input field. 

===

---
title: chrome.instanceID
url: https://developer.chrome.com/docs/extensions/reference/api/instanceID
---

# chrome.instanceID

## Description

Use `chrome.instanceID` to access the Instance ID service.

## Permissions

`gcm`

## Availability

Chrome 44+

## Methods

### `deleteID()`

Promise

```javascript
chrome.instanceID.deleteID(callback?: function)
```

Resets the app instance identifier and revokes all tokens associated with it.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  () => void
  ```

#### Returns

- `Promise<void>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `deleteToken()`

Promise

```javascript
chrome.instanceID.deleteToken(deleteTokenParams: object, callback?: function)
```

Revokes a granted token.

#### Parameters

- `deleteTokenParams` (object)
  Parameters for `deleteToken`.
  - `authorizedEntity` (string)
    Chrome 46+
    The authorized entity that is used to obtain the token.
  - `scope` (string)
    Chrome 46+
    The scope that is used to obtain the token.
- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  () => void
  ```

#### Returns

- `Promise<void>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getCreationTime()`

Promise

```javascript
chrome.instanceID.getCreationTime(callback?: function)
```

Retrieves the time when the InstanceID has been generated. The creation time will be returned by the callback.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (creationTime: number) => void
  ```
  - `creationTime` (number)
    The time when the Instance ID has been generated, represented in milliseconds since the epoch.

#### Returns

- `Promise<number>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getID()`

Promise

```javascript
chrome.instanceID.getID(callback?: function)
```

Retrieves an identifier for the app instance. The instance ID will be returned by the callback. The same ID will be returned as long as the application identity has not been revoked or expired.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (instanceID: string) => void
  ```
  - `instanceID` (string)
    An Instance ID assigned to the app instance.

#### Returns

- `Promise<string>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getToken()`

Promise

```javascript
chrome.instanceID.getToken(getTokenParams: object, callback?: function)
```

Return a token that allows the authorized entity to access the service defined by scope.

#### Parameters

- `getTokenParams` (object)
  Parameters for `getToken`.
  - `authorizedEntity` (string)
    Chrome 46+
    Identifies the entity that is authorized to access resources associated with this Instance ID. It can be a project ID from Google developer console.
  - `options` (object, optional)
    Chrome 46+ Deprecated since Chrome 89
    `options` are deprecated and will be ignored.
    Allows including a small number of string key/value pairs that will be associated with the token and may be used in processing the request.
  - `scope` (string)
    Chrome 46+
    Identifies authorized actions that the authorized entity can take. E.g. for sending GCM messages, GCM scope should be used.
- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (token: string) => void
  ```
  - `token` (string)
    A token assigned by the requested service.

#### Returns

- `Promise<string>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onTokenRefresh`

```javascript
chrome.instanceID.onTokenRefresh.addListener(callback: function)
```

Fired when all the granted tokens need to be refreshed.

#### Parameters

- `callback` (function)
  The callback parameter looks like:
  ```javascript
  () => void
  ```

===

---
title: chrome.loginState
url: https://developer.chrome.com/docs/extensions/reference/api/loginState
---

# `chrome.loginState`

Important: This API works only on ChromeOS.

## Description

Use the `chrome.loginState` API to read and monitor the login state.

## Permissions

`loginState`

## Availability

Chrome 78+ ChromeOS only

## Types

### `ProfileType`

#### Enum

*   `"SIGNIN_PROFILE"`: Specifies that the extension is in the signin profile.
*   `"USER_PROFILE"`: Specifies that the extension is in the user profile.

### `SessionState`

#### Enum

*   `"UNKNOWN"`: Specifies that the session state is unknown.
*   `"IN_OOBE_SCREEN"`: Specifies that the user is in the out-of-box-experience screen.
*   `"IN_LOGIN_SCREEN"`: Specifies that the user is in the login screen.
*   `"IN_SESSION"`: Specifies that the user is in the session.
*   `"IN_LOCK_SCREEN"`: Specifies that the user is in the lock screen.
*   `"IN_RMA_SCREEN"`: Specifies that the device is in RMA mode, finalizing repairs.

## Methods

### `getProfileType()`

`Promise`

```
chrome.loginState.getProfileType( callback?: function, )
```

Gets the type of the profile the extension is in.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: ProfileType) => void
    ```

    *   `result`: `ProfileType`

#### Returns

*   `Promise<ProfileType>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getSessionState()`

`Promise`

```
chrome.loginState.getSessionState( callback?: function, )
```

Gets the current session state.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: SessionState) => void
    ```

    *   `result`: `SessionState`

#### Returns

*   `Promise<SessionState>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onSessionStateChanged`

```
chrome.loginState.onSessionStateChanged.addListener( callback: function, )
```

Dispatched when the session state changes. `sessionState` is the new session state.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (sessionState: SessionState) => void
    ```

    *   `sessionState`: `SessionState` 

===

---
title: chrome.management
url: https://developer.chrome.com/docs/extensions/reference/api/management
---

# `chrome.management`

## Description

The `chrome.management` API provides ways to manage installed apps and extensions.

## Permissions

`management`

You must declare the "management" permission in the extension manifest to use the `management` API. For example:

```
{ "name": "My extension", ... "permissions": [ "management" ], ... }
```

`management.getPermissionWarningsByManifest()`, `management.uninstallSelf()`, and `management.getSelf()` do not require the `management` permission.

## Types

### `ExtensionDisabledReason`

Chrome 44+

A reason the item is disabled.

#### Enum

*   `"unknown"`
*   `"permissions_increase"`

### `ExtensionInfo`

Information about an installed extension, app, or theme.

#### Properties

*   `appLaunchUrl`: `string optional`

    The launch url (only present for apps).
*   `availableLaunchTypes`: `LaunchType[] optional`

    The currently available launch types (only present for apps).
*   `description`: `string`

    The description of this extension, app, or theme.
*   `disabledReason`: `ExtensionDisabledReason optional`

    A reason the item is disabled.
*   `enabled`: `boolean`

    Whether it is currently enabled or disabled.
*   `homepageUrl`: `string optional`

    The URL of the homepage of this extension, app, or theme.
*   `hostPermissions`: `string[]`

    Returns a list of host based permissions.
*   `icons`: `IconInfo[] optional`

    A list of icon information. Note that this just reflects what was declared in the manifest, and the actual image at that url may be larger or smaller than what was declared, so you might consider using explicit width and height attributes on `img` tags referencing these images. See the manifest documentation on `icons` for more details.
*   `id`: `string`

    The extension's unique identifier.
*   `installType`: `ExtensionInstallType`

    How the extension was installed.
*   `isApp`: `boolean`

    Deprecated

    Please use `management.ExtensionInfo.type`.

    True if this is an app.
*   `launchType`: `LaunchType optional`

    The app launch type (only present for apps).
*   `mayDisable`: `boolean`

    Whether this extension can be disabled or uninstalled by the user.
*   `mayEnable`: `boolean optional`

    Chrome 62+

    Whether this extension can be enabled by the user. This is only returned for extensions which are not enabled.
*   `name`: `string`

    The name of this extension, app, or theme.
*   `offlineEnabled`: `boolean`

    Whether the extension, app, or theme declares that it supports offline.
*   `optionsUrl`: `string`

    The url for the item's options page, if it has one.
*   `permissions`: `string[]`

    Returns a list of API based permissions.
*   `shortName`: `string`

    A short version of the name of this extension, app, or theme.
*   `type`: `ExtensionType`

    The type of this extension, app, or theme.
*   `updateUrl`: `string optional`

    The update URL of this extension, app, or theme.
*   `version`: `string`

    The version of this extension, app, or theme.
*   `versionName`: `string optional`

    Chrome 50+

    The version name of this extension, app, or theme if the manifest specified one.

### `ExtensionInstallType`

Chrome 44+

How the extension was installed. One of admin: The extension was installed because of an administrative policy, development: The extension was loaded unpacked in developer mode, normal: The extension was installed normally via a .crx file, sideload: The extension was installed by other software on the machine, other: The extension was installed by other means.

#### Enum

*   `"admin"`
*   `"development"`
*   `"normal"`
*   `"sideload"`
*   `"other"`

### `ExtensionType`

Chrome 44+

The type of this extension, app, or theme.

#### Enum

*   `"extension"`
*   `"hosted_app"`
*   `"packaged_app"`
*   `"legacy_packaged_app"`
*   `"theme"`
*   `"login_screen_extension"`

### `IconInfo`

Information about an icon belonging to an extension, app, or theme.

#### Properties

*   `size`: `number`

    A number representing the width and height of the icon. Likely values include (but are not limited to) 128, 48, 24, and 16.
*   `url`: `string`

    The URL for this icon image. To display a grayscale version of the icon (to indicate that an extension is disabled, for example), append `?grayscale=true` to the URL.

### `LaunchType`

These are all possible app launch types.

#### Enum

*   `"OPEN_AS_REGULAR_TAB"`
*   `"OPEN_AS_PINNED_TAB"`
*   `"OPEN_AS_WINDOW"`
*   `"OPEN_FULL_SCREEN"`

### `UninstallOptions`

Chrome 88+

Options for how to handle the extension's uninstallation.

#### Properties

*   `showConfirmDialog`: `boolean optional`

    Whether or not a confirm-uninstall dialog should prompt the user. Defaults to false for self uninstalls. If an extension uninstalls another extension, this parameter is ignored and the dialog is always shown.

## Methods

### `createAppShortcut()`

`Promise`

```
chrome.management.createAppShortcut( id: string, callback?: function, )
```

Display options to create shortcuts for an app. On Mac, only packaged app shortcuts can be created.

#### Parameters

*   `id`: `string`

    This should be the id from an app item of `management.ExtensionInfo`.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `generateAppForLink()`

`Promise`

```
chrome.management.generateAppForLink( url: string, title: chrome.string, callback?: function, )
```

Generate an app for a URL. Returns the generated bookmark app.

#### Parameters

*   `url`: `string`

    The URL of a web page. The scheme of the URL can only be "http" or "https".
*   `title`: `string`

    The title of the generated app.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: ExtensionInfo) => void
    ```

    *   `result`: `ExtensionInfo`

#### Returns

*   `Promise<ExtensionInfo>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `get()`

`Promise`

```
chrome.management.get( id: string, callback?: function, )
```

Returns information about the installed extension, app, or theme that has the given ID.

#### Parameters

*   `id`: `string`

    The ID from an item of `management.ExtensionInfo`.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: ExtensionInfo) => void
    ```

    *   `result`: `ExtensionInfo`

#### Returns

*   `Promise<ExtensionInfo>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAll()`

`Promise`

```
chrome.management.getAll( callback?: function, )
```

Returns a list of information about installed extensions and apps.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: ExtensionInfo[]) => void
    ```

    *   `result`: `ExtensionInfo[]`

#### Returns

*   `Promise<ExtensionInfo[]>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getPermissionWarningsById()`

`Promise`

```
chrome.management.getPermissionWarningsById( id: string, callback?: function, )
```

Returns a list of permission warnings for the given extension id.

#### Parameters

*   `id`: `string`

    The ID of an already installed extension.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (permissionWarnings: string[]) => void
    ```

    *   `permissionWarnings`: `string[]`

#### Returns

*   `Promise<string[]>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getPermissionWarningsByManifest()`

`Promise`

```
chrome.management.getPermissionWarningsByManifest( manifestStr: string, callback?: function, )
```

Returns a list of permission warnings for the given extension manifest string. Note: This function can be used without requesting the 'management' permission in the manifest.

#### Parameters

*   `manifestStr`: `string`

    Extension manifest JSON string.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (permissionWarnings: string[]) => void
    ```

    *   `permissionWarnings`: `string[]`

#### Returns

*   `Promise<string[]>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getSelf()`

`Promise`

```
chrome.management.getSelf( callback?: function, )
```

Returns information about the calling extension, app, or theme. Note: This function can be used without requesting the 'management' permission in the manifest.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: ExtensionInfo) => void
    ```

    *   `result`: `ExtensionInfo`

#### Returns

*   `Promise<ExtensionInfo>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `installReplacementWebApp()`

`Promise` Chrome 77+

```
chrome.management.installReplacementWebApp( callback?: function, )
```

Launches the `replacement_web_app` specified in the manifest. Prompts the user to install if not already installed.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `launchApp()`

`Promise`

```
chrome.management.launchApp( id: string, callback?: function, )
```

Launches an application.

#### Parameters

*   `id`: `string`

    The extension id of the application.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setEnabled()`

`Promise`

```
chrome.management.setEnabled( id: string, enabled: boolean, callback?: function, )
```

Enables or disables an app or extension. In most cases this function must be called in the context of a user gesture (e.g. an `onclick` handler for a button), and may present the user with a native confirmation UI as a way of preventing abuse.

#### Parameters

*   `id`: `string`

    This should be the id from an item of `management.ExtensionInfo`.
*   `enabled`: `boolean`

    Whether this item should be enabled or disabled.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setLaunchType()`

`Promise`

```
chrome.management.setLaunchType( id: string, launchType: LaunchType, callback?: function, )
```

Set the launch type of an app.

#### Parameters

*   `id`: `string`

    This should be the id from an app item of `management.ExtensionInfo`.
*   `launchType`: `LaunchType`

    The target launch type. Always check and make sure this launch type is in `ExtensionInfo.availableLaunchTypes`, because the available launch types vary on different platforms and configurations.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `uninstall()`

`Promise`

```
chrome.management.uninstall( id: string, options?: UninstallOptions, callback?: function, )
```

Uninstalls a currently installed app or extension. Note: This function does not work in managed environments when the user is not allowed to uninstall the specified extension/app. If the uninstall fails (e.g. the user cancels the dialog) the promise will be rejected or the callback will be called with `runtime.lastError` set.

#### Parameters

*   `id`: `string`

    This should be the id from an item of `management.ExtensionInfo`.
*   `options`: `UninstallOptions optional`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `uninstallSelf()`

`Promise`

```
chrome.management.uninstallSelf( options?: UninstallOptions, callback?: function, )
```

Uninstalls the calling extension. Note: This function can be used without requesting the 'management' permission in the manifest. This function does not work in managed environments when the user is not allowed to uninstall the specified extension/app.

#### Parameters

*   `options`: `UninstallOptions optional`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 88+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onDisabled`

```
chrome.management.onDisabled.addListener( callback: function, )
```

Fired when an app or extension has been disabled.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (info: ExtensionInfo) => void
    ```

    *   `info`: `ExtensionInfo`

### `onEnabled`

```
chrome.management.onEnabled.addListener( callback: function, )
```

Fired when an app or extension has been enabled.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (info: ExtensionInfo) => void
    ```

    *   `info`: `ExtensionInfo`

### `onInstalled`

```
chrome.management.onInstalled.addListener( callback: function, )
```

Fired when an app or extension has been installed.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (info: ExtensionInfo) => void
    ```

    *   `info`: `ExtensionInfo`

### `onUninstalled`

```
chrome.management.onUninstalled.addListener( callback: function, )
```

Fired when an app or extension has been uninstalled.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (id: string) => void
    ```

    *   `id`: `string` 

===

---
title: chrome.notifications
url: https://developer.chrome.com/docs/extensions/reference/api/notifications
---

# `chrome.notifications`

## Description

Use the `chrome.notifications` API to create rich notifications using templates and show these notifications to users in the system tray.

## Permissions

`notifications`

## Types

### `NotificationBitmap`

### `NotificationButton`

#### Properties

*   `iconUrl`: `string optional`

    Deprecated since Chrome 59

    Button icons not visible for Mac OS X users.
*   `title`: `string`

### `NotificationItem`

#### Properties

*   `message`: `string`

    Additional details about this item.
*   `title`: `string`

    Title of one item of a list notification.

### `NotificationOptions`

#### Properties

*   `appIconMaskUrl`: `string optional`

    Deprecated since Chrome 59

    The app icon mask is not visible for Mac OS X users.

    A URL to the app icon mask. URLs have the same restrictions as `iconUrl`.

    The app icon mask should be in alpha channel, as only the alpha channel of the image will be considered.
*   `buttons`: `NotificationButton[] optional`

    Text and icons for up to two notification action buttons.
*   `contextMessage`: `string optional`

    Alternate notification content with a lower-weight font.
*   `eventTime`: `number optional`

    A timestamp associated with the notification, in milliseconds past the epoch (e.g. `Date.now() + n`).
*   `iconUrl`: `string optional`

    A URL to the sender's avatar, app icon, or a thumbnail for image notifications.

    URLs can be a data URL, a blob URL, or a URL relative to a resource within this extension's .crx file

    \*\*Note:\*\*This value is required for the `notifications.create()` method.
*   `imageUrl`: `string optional`

    Deprecated since Chrome 59

    The image is not visible for Mac OS X users.

    A URL to the image thumbnail for image-type notifications. URLs have the same restrictions as `iconUrl`.
*   `isClickable`: `boolean optional`

    Deprecated since Chrome 67

    This UI hint is ignored as of Chrome 67
*   `items`: `NotificationItem[] optional`

    Items for multi-item notifications. Users on Mac OS X only see the first item.
*   `message`: `string optional`

    Main notification content.

    \*\*Note:\*\*This value is required for the `notifications.create()` method.
*   `priority`: `number optional`

    Priority ranges from -2 to 2. -2 is lowest priority. 2 is highest. Zero is default. On platforms that don't support a notification center (Windows, Linux & Mac), -2 and -1 result in an error as notifications with those priorities will not be shown at all.
*   `progress`: `number optional`

    Current progress ranges from 0 to 100.
*   `requireInteraction`: `boolean optional`

    Chrome 50+

    Indicates that the notification should remain visible on screen until the user activates or dismisses the notification. This defaults to false.
*   `silent`: `boolean optional`

    Chrome 70+

    Indicates that no sounds or vibrations should be made when the notification is being shown. This defaults to false.
*   `title`: `string optional`

    Title of the notification (e.g. sender name for email).

    \*\*Note:\*\*This value is required for the `notifications.create()` method.
*   `type`: `TemplateType optional`

    Which type of notification to display. Required for `notifications.create` method.

### `PermissionLevel`

#### Enum

*   `"granted"`: Specifies that the user has elected to show notifications from the app or extension. This is the default at install time.
*   `"denied"`: Specifies that the user has elected not to show notifications from the app or extension.

### `TemplateType`

#### Enum

*   `"basic"`: Contains an icon, title, message, expandedMessage, and up to two buttons.
*   `"image"`: Contains an icon, title, message, expandedMessage, image, and up to two buttons.
*   `"list"`: Contains an icon, title, message, items, and up to two buttons. Users on Mac OS X only see the first item.
*   `"progress"`: Contains an icon, title, message, progress, and up to two buttons.

## Methods

### `clear()`

`Promise`

```
chrome.notifications.clear( notificationId: string, callback?: function, )
```

Clears the specified notification.

#### Parameters

*   `notificationId`: `string`

    The id of the notification to be cleared. This is returned by `notifications.create` method.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (wasCleared: boolean) => void
    ```

    *   `wasCleared`: `boolean`

#### Returns

*   `Promise<boolean>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `create()`

`Promise`

```
chrome.notifications.create( notificationId?: string, options: NotificationOptions, callback?: function, )
```

Creates and displays a notification.

#### Parameters

*   `notificationId`: `string optional`

    Identifier of the notification. If not set or empty, an ID will automatically be generated. If it matches an existing notification, this method first clears that notification before proceeding with the create operation. The identifier may not be longer than 500 characters.

    The `notificationId` parameter is required before Chrome 42.
*   `options`: `NotificationOptions`

    Contents of the notification.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (notificationId: string) => void
    ```

    *   `notificationId`: `string`

#### Returns

*   `Promise<string>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAll()`

`Promise`

```
chrome.notifications.getAll( callback?: function, )
```

Retrieves all the notifications of this app or extension.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (notifications: object) => void
    ```

    *   `notifications`: `object`

#### Returns

*   `Promise<object>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getPermissionLevel()`

`Promise`

```
chrome.notifications.getPermissionLevel( callback?: function, )
```

Retrieves whether the user has enabled notifications from this app or extension.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (level: PermissionLevel) => void
    ```

    *   `level`: `PermissionLevel`

#### Returns

*   `Promise<PermissionLevel>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `update()`

`Promise`

```
chrome.notifications.update( notificationId: string, options: NotificationOptions, callback?: function, )
```

Updates an existing notification.

#### Parameters

*   `notificationId`: `string`

    The id of the notification to be updated. This is returned by `notifications.create` method.
*   `options`: `NotificationOptions`

    Contents of the notification to update to.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (wasUpdated: boolean) => void
    ```

    *   `wasUpdated`: `boolean`

#### Returns

*   `Promise<boolean>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onButtonClicked`

```
chrome.notifications.onButtonClicked.addListener( callback: function, )
```

The user pressed a button in the notification.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (notificationId: string, buttonIndex: number) => void
    ```

    *   `notificationId`: `string`
    *   `buttonIndex`: `number`

### `onClicked`

```
chrome.notifications.onClicked.addListener( callback: function, )
```

The user clicked in a non-button area of the notification.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (notificationId: string) => void
    ```

    *   `notificationId`: `string`

### `onClosed`

```
chrome.notifications.onClosed.addListener( callback: function, )
```

The notification closed, either by the system or by user action.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (notificationId: string, byUser: boolean) => void
    ```

    *   `notificationId`: `string`
    *   `byUser`: `boolean`

### `onPermissionLevelChanged`

```
chrome.notifications.onPermissionLevelChanged.addListener( callback: function, )
```

The user changes the permission level. As of Chrome 47, only ChromeOS has UI that dispatches this event.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (level: PermissionLevel) => void
    ```

    *   `level`: `PermissionLevel`

### `onShowSettings`

Deprecated since Chrome 65

```
chrome.notifications.onShowSettings.addListener( callback: function, )
```

Custom notification settings button is no longer supported.

The user clicked on a link for the app's notification settings. As of Chrome 47, only ChromeOS has UI that dispatches this event. As of Chrome 65, that UI has been removed from ChromeOS, too.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    () => void
    ``` 

===

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

===

---
title: chrome.omnibox
url: https://developer.chrome.com/docs/extensions/reference/api/omnibox
---

# `chrome.omnibox`

## Description

The `omnibox` API allows you to register a keyword with Google Chrome's address bar, which is also known as the omnibox.

When the user enters your extension's keyword, the user starts interacting solely with your extension. Each keystroke is sent to your extension, and you can provide suggestions in response.

The suggestions can be richly formatted in a variety of ways. When the user accepts a suggestion, your extension is notified and can take action.

## Manifest

The following keys must be declared in the manifest to use this API.

`"omnibox"`

You must include an `"omnibox.keyword"` field in the manifest to use the `omnibox` API. You should also specify a 16 by 16-pixel icon, which will be displayed in the address bar when suggesting that users enter keyword mode.

For example:

```
{ "name": "Aaron's omnibox extension", "version": "1.0", "omnibox": { "keyword" : "aaron" }, "icons": { "16": "16-full-color.png" }, "background": { "persistent": false, "scripts": ["background.js"] } }
```

Note: Chrome automatically creates a grayscale version of your 16x16-pixel icon. You should provide a full-color version so that it can also be used in other situations that require color. For example, the `contextMenus` API also uses a 16x16-pixel icon, but it is displayed in color.

## Examples

To try this API, install the omnibox API example from the [chrome-extension-samples](https://github.com/GoogleChrome/chrome-extensions-samples) repository.

## Types

### `DefaultSuggestResult`

A suggest result.

#### Properties

*   `description`: `string`

    The text that is displayed in the URL dropdown. Can contain XML-style markup for styling. The supported tags are `'url'` (for a literal URL), `'match'` (for highlighting text that matched what the user's query), and `'dim'` (for dim helper text). The styles can be nested, eg. dimmed match.

### `DescriptionStyleType`

Chrome 44+

The style type.

#### Enum

*   `"url"`
*   `"match"`
*   `"dim"`

### `OnInputEnteredDisposition`

Chrome 44+

The window disposition for the omnibox query. This is the recommended context to display results. For example, if the omnibox command is to navigate to a certain URL, a disposition of `'newForegroundTab'` means the navigation should take place in a new selected tab.

#### Enum

*   `"currentTab"`
*   `"newForegroundTab"`
*   `"newBackgroundTab"`

### `SuggestResult`

A suggest result.

#### Properties

*   `content`: `string`

    The text that is put into the URL bar, and that is sent to the extension when the user chooses this entry.
*   `deletable`: `boolean optional`

    Chrome 63+

    Whether the suggest result can be deleted by the user.
*   `description`: `string`

    The text that is displayed in the URL dropdown. Can contain XML-style markup for styling. The supported tags are `'url'` (for a literal URL), `'match'` (for highlighting text that matched what the user's query), and `'dim'` (for dim helper text). The styles can be nested, eg. dimmed match. You must escape the five predefined entities to display them as text: [stackoverflow.com/a/1091953/89484](https://stackoverflow.com/a/1091953/89484)

## Methods

### `setDefaultSuggestion()`

`Promise`

```
chrome.omnibox.setDefaultSuggestion( suggestion: DefaultSuggestResult, callback?: function, )
```

Sets the description and styling for the default suggestion. The default suggestion is the text that is displayed in the first suggestion row underneath the URL bar.

#### Parameters

*   `suggestion`: `DefaultSuggestResult`

    A partial `SuggestResult` object, without the `'content'` parameter.
*   `callback`: `function optional`

    Chrome 100+

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 100+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onDeleteSuggestion`

Chrome 63+

```
chrome.omnibox.onDeleteSuggestion.addListener( callback: function, )
```

User has deleted a suggested result.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (text: string) => void
    ```

    *   `text`: `string`

### `onInputCancelled`

```
chrome.omnibox.onInputCancelled.addListener( callback: function, )
```

User has ended the keyword input session without accepting the input.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    () => void
    ```

### `onInputChanged`

```
chrome.omnibox.onInputChanged.addListener( callback: function, )
```

User has changed what is typed into the omnibox.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (text: string, suggest: function) => void
    ```

    *   `text`: `string`
    *   `suggest`: `function`

    The `suggest` parameter looks like:

    ```
    (suggestResults: SuggestResult[]) => void
    ```

    *   `suggestResults`: `SuggestResult[]`

        Array of suggest results

### `onInputEntered`

```
chrome.omnibox.onInputEntered.addListener( callback: function, )
```

User has accepted what is typed into the omnibox.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (text: string, disposition: OnInputEnteredDisposition) => void
    ```

    *   `text`: `string`
    *   `disposition`: `OnInputEnteredDisposition`

### `onInputStarted`

```
chrome.omnibox.onInputStarted.addListener( callback: function, )
```

User has started a keyword input session by typing the extension's keyword. This is guaranteed to be sent exactly once per input session, and before any `onInputChanged` events.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    () => void
    ``` 

===

---
title: chrome.pageCapture
url: https://developer.chrome.com/docs/extensions/reference/api/pageCapture
---

# `chrome.pageCapture`

## Description

Use the `chrome.pageCapture` API to save a tab as MHTML.

MHTML is a standard format supported by most browsers. It encapsulates in a single file a page and all its resources (CSS files, images..).

Note that for security reasons a MHTML file can only be loaded from the file system and that it can only be loaded in the main frame.

## Permissions

`pageCapture`

You must declare the `"pageCapture"` permission in the extension manifest to use the `pageCapture` API. For example:

```
{ "name": "My extension", ... "permissions": [ "pageCapture" ], ... }
```

## Methods

### `saveAsMHTML()`

`Promise`

```
chrome.pageCapture.saveAsMHTML( details: object, callback?: function, )
```

Saves the content of the tab with given id as MHTML.

#### Parameters

*   `details`: `object`

    *   `tabId`: `number`

        The id of the tab to save as MHTML.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (mhtmlData?: Blob) => void
    ```

    *   `mhtmlData`: `Blob optional`

        The MHTML data as a `Blob`.

#### Returns

*   `Promise<Blob | undefined>`: Chrome 116+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.permissions
url: https://developer.chrome.com/docs/extensions/reference/api/permissions
---

# `chrome.permissions`

## Description

Use the `chrome.permissions` API to request declared optional permissions at run time rather than install time, so users understand why the permissions are needed and grant only those that are necessary.

## Concepts and usage

Permission warnings exist to describe the capabilities granted by an API, but some of these warnings may not be obvious. The `Permissions` API allows developers to explain permission warnings and introduce new features gradually which gives users a risk-free introduction to the extension. This way, users can specify how much access they are willing to grant and which features they want to enable.

For example, the [optional permissions extension](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api-samples/optional-permissions) core functionality is overriding the new tab page. One feature is displaying the user's goal of the day. This feature only requires the `storage` permission, which does not include a warning. The extension has an additional feature, that users can enable by clicking the following button:

An extension button that enables additional features.

Displaying the user's top sites requires the `topSites` permission, which has the following warning.

An extension warning for topSites API

### Implement optional permissions

#### Step 1: Decide which permissions are required and which are optional

An extension can declare both required and optional permissions. In general, you should:

*   Use required permissions when they are needed for your extension's basic functionality.
*   Use optional permissions when they are needed for optional features in your extension.

Advantages of required permissions:

*   Fewer prompts: An extension can prompt the user once to accept all permissions.
*   Simpler development: Required permissions are guaranteed to be present.

Advantages of optional permissions:

*   Better security: Extensions run with fewer permissions since users only enable permissions that are needed.
*   Better information for users: An extension can explain why it needs a particular permission when the user enables the relevant feature.
*   Easier upgrades: When you upgrade your extension, Chrome won't disable it for your users if the upgrade adds optional rather than required permissions.

#### Step 2: Declare optional permissions in the manifest

Declare optional permissions in your extension manifest with the `optional_permissions` key, using the same format as the `permissions` field:

```
{ "name": "My extension", ... "optional_permissions": ["tabs"], "optional_host_permissions": ["https://www.google.com/"], ... }
```

If you want to request hosts that you only discover at runtime, include `"https://*/*"` in your extension's `optional_host_permissions` field. This lets you specify any origin in `"Permissions.origins"` as long as it has a matching scheme.

Permissions that can not be specified as optional

Most Chrome extension permissions can be specified as optional, with the following exceptions.

| Permission             | Description                                                                                                  |
| :--------------------- | :----------------------------------------------------------------------------------------------------------- |
| `"debugger"`           | The `chrome.debugger` API serves as an alternate transport for Chrome's remote debugging protocol.             |
| `"declarativeNetRequest"` | Grants the extension access to the `chrome.declarativeNetRequest` API.                                       |
| `"devtools"`           | Allows extension to expand Chrome DevTools functionality.                                                    |
| `"geolocation"`        | Allows the extension to use the HTML5 geolocation API.                                                       |
| `"mdns"`               | Grants the extension access to the `chrome.mdns` API.                                                        |
| `"proxy"`              | Grants the extension access to the `chrome.proxy` API to manage Chrome's proxy settings.                     |
| `"tts"`                | The `chrome.tts` API plays synthesized text-to-speech (TTS).                                                 |
| `"ttsEngine"`          | The `chrome.ttsEngine` API implements a text-to-speech (TTS) engine using an extension.                      |
| `"wallpaper"`          | ChromeOS only. Use the `chrome.wallpaper` API change the ChromeOS wallpaper.                                 |

View [Declare Permissions](https://developer.chrome.com/docs/extensions/develop/concepts/declare-permissions) for further information on available permissions and their warnings.

#### Step 3: Request optional permissions

Request the permissions from within a user gesture using `permissions.request()`:

```
document.querySelector('#my-button').addEventListener('click', (event) => { // Permissions must be requested from inside a user gesture, like a button's // click handler. chrome.permissions.request({ permissions: ['tabs'], origins: ['https://www.google.com/'] }, (granted) => { // The callback argument will be true if the user granted the permissions. if (granted) { doSomething(); } else { doSomethingElse(); } }); });
```

Chrome prompts the user if adding the permissions results in different warning messages than the user has already seen and accepted. For example, the previous code might result in a prompt like this:

An example permission confirmation prompt.

#### Step 4: Check the extension's current permissions

To check whether your extension has a specific permission or set of permissions, use `permission.contains()`:

```
chrome.permissions.contains({ permissions: ['tabs'], origins: ['https://www.google.com/'] }, (result) => { if (result) { // The extension has the permissions. } else { // The extension doesn't have the permissions. } });
```

#### Step 5: Remove the permissions

You should remove permissions when you no longer need them. After a permission has been removed, calling `permissions.request()` usually adds the permission back without prompting the user.

```
chrome.permissions.remove({ permissions: ['tabs'], origins: ['https://www.google.com/'] }, (removed) => { if (removed) { // The permissions have been removed. } else { // The permissions have not been removed (e.g., you tried to remove // required permissions). } });
```

## Types

### `Permissions`

#### Properties

*   `origins`: `string[] optional`

    The list of host permissions, including those specified in the `optional_permissions` or `permissions` keys in the manifest, and those associated with Content Scripts.
*   `permissions`: `string[] optional`

    List of named permissions (does not include hosts or origins).

## Methods

### `addHostAccessRequest()`

`Promise` Chrome 133+ MV3+

```
chrome.permissions.addHostAccessRequest( request: object, callback?: function, )
```

Adds a host access request. Request will only be signaled to the user if extension can be granted access to the host in the request. Request will be reset on cross-origin navigation. When accepted, grants persistent access to the site's top origin

#### Parameters

*   `request`: `object`

    *   `documentId`: `string optional`

        The id of a document where host access requests can be shown. Must be the top-level document within a tab. If provided, the request is shown on the tab of the specified document and is removed when the document navigates to a new origin. Adding a new request will override any existent request for `tabId`. This or `tabId` must be specified.
    *   `pattern`: `string optional`

        The URL pattern where host access requests can be shown. If provided, host access requests will only be shown on URLs that match this pattern.
    *   `tabId`: `number optional`

        The id of the tab where host access requests can be shown. If provided, the request is shown on the specified tab and is removed when the tab navigates to a new origin. Adding a new request will override an existent request for `documentId`. This or `documentId` must be specified.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `contains()`

`Promise`

```
chrome.permissions.contains( permissions: Permissions, callback?: function, )
```

Checks if the extension has the specified permissions.

#### Parameters

*   `permissions`: `Permissions`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: boolean) => void
    ```

    *   `result`: `boolean`

        True if the extension has the specified permissions. If an origin is specified as both an optional permission and a content script match pattern, this will return false unless both permissions are granted.

#### Returns

*   `Promise<boolean>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getAll()`

`Promise`

```
chrome.permissions.getAll( callback?: function, )
```

Gets the extension's current set of permissions.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (permissions: Permissions) => void
    ```

    *   `permissions`: `Permissions`

        The extension's active permissions. Note that the `origins` property will contain granted origins from those specified in the `permissions` and `optional_permissions` keys in the manifest and those associated with Content Scripts.

#### Returns

*   `Promise<Permissions>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `remove()`

`Promise`

```
chrome.permissions.remove( permissions: Permissions, callback?: function, )
```

Removes access to the specified permissions. If there are any problems removing the permissions, `runtime.lastError` will be set.

#### Parameters

*   `permissions`: `Permissions`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (removed: boolean) => void
    ```

    *   `removed`: `boolean`

        True if the permissions were removed.

#### Returns

*   `Promise<boolean>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `removeHostAccessRequest()`

`Promise` Chrome 133+ MV3+

```
chrome.permissions.removeHostAccessRequest( request: object, callback?: function, )
```

Removes a host access request, if existent.

#### Parameters

*   `request`: `object`

    *   `documentId`: `string optional`

        The id of a document where host access request will be removed. Must be the top-level document within a tab. This or `tabId` must be specified.
    *   `pattern`: `string optional`

        The URL pattern where host access request will be removed. If provided, this must exactly match the pattern of an existing host access request.
    *   `tabId`: `number optional`

        The id of the tab where host access request will be removed. This or `documentId` must be specified.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`: Chrome 133+ MV3+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `request()`

`Promise`

```
chrome.permissions.request( permissions: Permissions, callback?: function, )
```

Requests access to the specified permissions, displaying a prompt to the user if necessary. These permissions must either be defined in the `optional_permissions` field of the manifest or be required permissions that were withheld by the user. Paths on origin patterns will be ignored. You can request subsets of optional origin permissions; for example, if you specify `*://*/*` in the `optional_permissions` section of the manifest, you can request `http://example.com/`. If there are any problems requesting the permissions, `runtime.lastError` will be set.

#### Parameters

*   `permissions`: `Permissions`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (granted: boolean) => void
    ```

    *   `granted`: `boolean`

        True if the user granted the specified permissions.

#### Returns

*   `Promise<boolean>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onAdded`

```
chrome.permissions.onAdded.addListener( callback: function, )
```

Fired when the extension acquires new permissions.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (permissions: Permissions) => void
    ```

    *   `permissions`: `Permissions`

### `onRemoved`

```
chrome.permissions.onRemoved.addListener( callback: function, )
```

Fired when access to permissions has been removed from the extension.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (permissions: Permissions) => void
    ```

    *   `permissions`: `Permissions` 

===

---
title: chrome.platformKeys
url: https://developer.chrome.com/docs/extensions/reference/api/platformKeys
---

# `chrome.platformKeys`

Important: This API works only on ChromeOS.

## Description

Use the `chrome.platformKeys` API to access client certificates managed by the platform. If the user or policy grants the permission, an extension can use such a certficate in its custom authentication protocol. E.g. this allows usage of platform managed certificates in third party VPNs (see `chrome.vpnProvider`).

## Permissions

`platformKeys`

## Availability

Chrome 45+ ChromeOS only

## Types

### `ClientCertificateRequest`

#### Properties

*   `certificateAuthorities`: `ArrayBuffer[]`

    List of distinguished names of certificate authorities allowed by the server. Each entry must be a DER-encoded X.509 DistinguishedName.
*   `certificateTypes`: `ClientCertificateType[]`

    This field is a list of the types of certificates requested, sorted in order of the server's preference. Only certificates of a type contained in this list will be retrieved. If `certificateTypes` is the empty list, however, certificates of any type will be returned.

### `ClientCertificateType`

#### Enum

*   `"rsaSign"`
*   `"ecdsaSign"`

### `Match`

#### Properties

*   `certificate`: `ArrayBuffer`

    The DER encoding of a X.509 certificate.
*   `keyAlgorithm`: `object`

    The `KeyAlgorithm` of the certified key. This contains algorithm parameters that are inherent to the key of the certificate (e.g. the key length). Other parameters like the hash function used by the sign function are not included.

### `SelectDetails`

#### Properties

*   `clientCerts`: `ArrayBuffer[] optional`

    If given, the `selectClientCertificates` operates on this list. Otherwise, obtains the list of all certificates from the platform's certificate stores that are available to this extensions. Entries that the extension doesn't have permission for or which doesn't match the request, are removed.
*   `interactive`: `boolean`

    If true, the filtered list is presented to the user to manually select a certificate and thereby granting the extension access to the certificate(s) and key(s). Only the selected certificate(s) will be returned. If is false, the list is reduced to all certificates that the extension has been granted access to (automatically or manually).
*   `request`: `ClientCertificateRequest`

    Only certificates that match this request will be returned.

### `VerificationDetails`

#### Properties

*   `hostname`: `string`

    The hostname of the server to verify the certificate for, e.g. the server that presented the `serverCertificateChain`.
*   `serverCertificateChain`: `ArrayBuffer[]`

    Each chain entry must be the DER encoding of a X.509 certificate, the first entry must be the server certificate and each entry must certify the entry preceding it.

### `VerificationResult`

#### Properties

*   `debug_errors`: `string[]`

    If the trust verification failed, this array contains the errors reported by the underlying network layer. Otherwise, this array is empty.

    Note: This list is meant for debugging only and may not contain all relevant errors. The errors returned may change in future revisions of this API, and are not guaranteed to be forwards or backwards compatible.
*   `trusted`: `boolean`

    The result of the trust verification: true if trust for the given verification details could be established and false if trust is rejected for any reason.

## Methods

### `getKeyPair()`

```
chrome.platformKeys.getKeyPair( certificate: ArrayBuffer, parameters: object, callback: function, )
```

Passes the key pair of `certificate` for usage with `platformKeys.subtleCrypto` to `callback`.

#### Parameters

*   `certificate`: `ArrayBuffer`

    The certificate of a `Match` returned by `selectClientCertificates`.
*   `parameters`: `object`

    Determines signature/hash algorithm parameters additionally to the parameters fixed by the key itself. The same parameters are accepted as by WebCrypto's `importKey` function, e.g. `RsaHashedImportParams` for a RSASSA-PKCS1-v1_5 key and `EcKeyImportParams` for EC key. Additionally for RSASSA-PKCS1-v1_5 keys, hashing algorithm name parameter can be specified with one of the following values: `"none"`, `"SHA-1"`, `"SHA-256"`, `"SHA-384"`, or `"SHA-512"`, e.g. `{"hash": { "name": "none" } }`. The sign function will then apply PKCS#1 v1.5 padding but not hash the given data.

    Currently, this method only supports the `"RSASSA-PKCS1-v1_5"` and `"ECDSA"` algorithms.
*   `callback`: `function`

    The callback parameter looks like:

    ```
    (publicKey: object, privateKey?: object) => void
    ```

    *   `publicKey`: `object`
    *   `privateKey`: `object optional`

        Might be null if this extension does not have access to it.

### `getKeyPairBySpki()`

Chrome 85+

```
chrome.platformKeys.getKeyPairBySpki( publicKeySpkiDer: ArrayBuffer, parameters: object, callback: function, )
```

Passes the key pair identified by `publicKeySpkiDer` for usage with `platformKeys.subtleCrypto` to `callback`.

#### Parameters

*   `publicKeySpkiDer`: `ArrayBuffer`

    A DER-encoded X.509 SubjectPublicKeyInfo, obtained e.g. by calling WebCrypto's `exportKey` function with `format="spki"`.
*   `parameters`: `object`

    Provides signature and hash algorithm parameters, in addition to those fixed by the key itself. The same parameters are accepted as by WebCrypto's `importKey` function, e.g. `RsaHashedImportParams` for a RSASSA-PKCS1-v1_5 key. For RSASSA-PKCS1-v1_5 keys, we need to also pass a `"hash"` parameter `{ "hash": { "name": string } }`. The `"hash"` parameter represents the name of the hashing algorithm to be used in the digest operation before a sign. It is possible to pass `"none"` as the hash name, in which case the sign function will apply PKCS#1 v1.5 padding and but not hash the given data.

    Currently, this method supports the `"ECDSA"` algorithm with named-curve P-256 and `"RSASSA-PKCS1-v1_5"` algorithm with one of the hashing algorithms `"none"`, `"SHA-1"`, `"SHA-256"`, `"SHA-384"`, and `"SHA-512"`.
*   `callback`: `function`

    The callback parameter looks like:

    ```
    (publicKey: object, privateKey?: object) => void
    ```

    *   `publicKey`: `object`
    *   `privateKey`: `object optional`

        Might be null if this extension does not have access to it.

### `selectClientCertificates()`

`Promise`

```
chrome.platformKeys.selectClientCertificates( details: SelectDetails, callback?: function, )
```

This method filters from a list of client certificates the ones that are known to the platform, match request and for which the extension has permission to access the certificate and its private key. If `interactive` is true, the user is presented a dialog where they can select from matching certificates and grant the extension access to the certificate(s) and key(s). Only the selected certificate(s) will be returned. If is false, the list is reduced to all certificates that the extension has been granted access to (automatically or manually).

#### Parameters

*   `details`: `SelectDetails`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (matches: Match[]) => void
    ```

    *   `matches`: `Match[]`

        The list of certificates that match the request, that the extension has permission for and, if `interactive` is true, that were selected by the user.

#### Returns

*   `Promise<Match[]>`: Chrome 121+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `subtleCrypto()`

```
chrome.platformKeys.subtleCrypto()
```

An implementation of WebCrypto's `SubtleCrypto` that allows crypto operations on keys of client certificates that are available to this extension.

#### Returns

*   `object | undefined`

### `verifyTLSServerCertificate()`

`Promise`

```
chrome.platformKeys.verifyTLSServerCertificate( details: VerificationDetails, callback?: function, )
```

Checks whether `details.serverCertificateChain` can be trusted for `details.hostname` according to the trust settings of the platform. Note: The actual behavior of the trust verification is not fully specified and might change in the future. The API implementation verifies certificate expiration, validates the certification path and checks trust by a known CA. The implementation is supposed to respect the EKU serverAuth and to support subject alternative names.

#### Parameters

*   `details`: `VerificationDetails`
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (result: VerificationResult) => void
    ```

    *   `result`: `VerificationResult`

#### Returns

*   `Promise<VerificationResult>`: Chrome 121+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.power
url: https://developer.chrome.com/docs/extensions/reference/api/power
---

# `chrome.power`

## Description

Use the `chrome.power` API to override the system's power management features.

## Permissions

`power`

## Concepts and usage

By default, operating systems dim the screen when users are inactive and eventually suspend the system. With the `power` API, an app or extension can keep the system awake.

Using this API, you can specify the `Level` to which power management is disabled. The `"system"` level keeps the system active, but allows the screen to be dimmed or turned off. For example, a communication app can continue to receive messages while the screen is off. The `"display"` level keeps the screen and system active. E-book and presentation apps, for example, can keep the screen and system active while users read.

When a user has more than one app or extension active, each with its own power level, the highest-precedence level takes effect; `"display"` always takes precedence over `"system"`. For example, if app A asks for `"system"` power management, and app B asks for `"display"`, `"display"` is used until app B is unloaded or releases its request. If app A is still active, `"system"` is then used.

## Types

### `Level`

#### Enum

*   `"system"`: Prevents the system from sleeping in response to user inactivity.
*   `"display"`: Prevents the display from being turned off or dimmed, or the system from sleeping in response to user inactivity.

## Methods

### `releaseKeepAwake()`

```
chrome.power.releaseKeepAwake()
```

Releases a request previously made via `requestKeepAwake()`.

### `reportActivity()`

`Promise` Chrome 113+ ChromeOS only

```
chrome.power.reportActivity( callback?: function, )
```

Reports a user activity in order to awake the screen from a dimmed or turned off state or from a screensaver. Exits the screensaver if it is currently active.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `requestKeepAwake()`

```
chrome.power.requestKeepAwake( level: Level, )
```

Requests that power management be temporarily disabled. `level` describes the degree to which power management should be disabled. If a request previously made by the same app is still active, it will be replaced by the new request.

#### Parameters

*   `level`: `Level` 

===

---
title: chrome.printerProvider
url: https://developer.chrome.com/docs/extensions/reference/api/printerProvider
---

# `chrome.printerProvider`

## Description

The `chrome.printerProvider` API exposes events used by print manager to query printers controlled by extensions, to query their capabilities and to submit print jobs to these printers.

## Permissions

`printerProvider`

## Availability

Chrome 44+

## Types

### `PrinterInfo`

#### Properties

*   `description`: `string optional`

    Printer's human readable description.
*   `id`: `string`

    Unique printer ID.
*   `name`: `string`

    Printer's human readable name.

### `PrintError`

Error codes returned in response to `onPrintRequested` event.

#### Enum

*   `"OK"`: Specifies that the operation was completed successfully.
*   `"FAILED"`: Specifies that a general failure occured.
*   `"INVALID_TICKET"`: Specifies that the print ticket is invalid. For example, the ticket is inconsistent with some capabilities, or the extension is not able to handle all settings from the ticket.
*   `"INVALID_DATA"`: Specifies that the document is invalid. For example, data may be corrupted or the format is incompatible with the extension.

### `PrintJob`

#### Properties

*   `contentType`: `string`

    The document content type. Supported formats are `"application/pdf"` and `"image/pwg-raster"`.
*   `document`: `Blob`

    Blob containing the document data to print. Format must match `contentType`.
*   `printerId`: `string`

    ID of the printer which should handle the job.
*   `ticket`: `object`

    Print ticket in CJT format.

    The CJT reference is marked as deprecated. It is deprecated for Google Cloud Print only. is not deprecated for ChromeOS printing.
*   `title`: `string`

    The print job title.

## Events

### `onGetCapabilityRequested`

```
chrome.printerProvider.onGetCapabilityRequested.addListener( callback: function, )
```

Event fired when print manager requests printer capabilities.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (printerId: string, resultCallback: function) => void
    ```

    *   `printerId`: `string`
    *   `resultCallback`: `function`

    The `resultCallback` parameter looks like:

    ```
    (capabilities: object) => void
    ```

    *   `capabilities`: `object`

        Device capabilities in CDD format.

### `onGetPrintersRequested`

```
chrome.printerProvider.onGetPrintersRequested.addListener( callback: function, )
```

Event fired when print manager requests printers provided by extensions.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (resultCallback: function) => void
    ```

    *   `resultCallback`: `function`

    The `resultCallback` parameter looks like:

    ```
    (printerInfo: PrinterInfo[]) => void
    ```

    *   `printerInfo`: `PrinterInfo[]`

### `onGetUsbPrinterInfoRequested`

Chrome 45+

```
chrome.printerProvider.onGetUsbPrinterInfoRequested.addListener( callback: function, )
```

Event fired when print manager requests information about a USB device that may be a printer.

Note: An application should not rely on this event being fired more than once per device. If a connected device is supported it should be returned in the `onGetPrintersRequested` event.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (device: usb.Device, resultCallback: function) => void
    ```

    *   `device`: `usb.Device`
    *   `resultCallback`: `function`

    The `resultCallback` parameter looks like:

    ```
    (printerInfo?: PrinterInfo) => void
    ```

    *   `printerInfo`: `PrinterInfo optional`

### `onPrintRequested`

```
chrome.printerProvider.onPrintRequested.addListener( callback: function, )
```

Event fired when print manager requests printing.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (printJob: PrintJob, resultCallback: function) => void
    ```

    *   `printJob`: `PrintJob`
    *   `resultCallback`: `function`

    The `resultCallback` parameter looks like:

    ```
    (result: PrintError) => void
    ```

    *   `result`: `PrintError` 

===

---
title: chrome.printing
url: https://developer.chrome.com/docs/extensions/reference/api/printing
---

Important: This API works only on ChromeOS.

## Description

Use the `chrome.printing` API to send print jobs to printers installed on Chromebook.

## Permissions

`printing`

## Availability

Chrome 81+ ChromeOS only

All `chrome.printing` methods and events require you to declare the "printing" permission in the extension manifest. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "printing"
  ],
  ...
}
```

## Examples

The examples below demonstrate using each of the methods in the printing namespace. This code is copied from or based on the api-samples/printing in the extensions-samples Github repo.

### cancelJob()

This example uses the `onJobStatusChanged` handler to hide a 'cancel' button when the `jobStatus` is neither `PENDING` or `IN_PROGRESS`. Note that on some networks or when a Chromebook is connected directly to the printer, these states may pass too quickly for the cancel button to be visible long enough to be called. This is greatly simplified printing example.

```javascript
chrome.printing.onJobStatusChanged.addListener((jobId, status) => {
  const cancelButton = document.getElementById("cancelButton");
  cancelButton.addEventListener('click', () => {
    chrome.printing.cancelJob(jobId).then((response) => {
      if (response !== undefined) {
        console.log(response.status);
      }
      if (chrome.runtime.lastError !== undefined) {
        console.log(chrome.runtime.lastError.message);
      }
    });
  });
  if (status !== "PENDING" && status !== "IN_PROGRESS") {
    cancelButton.style.visibility = 'hidden';
  } else {
    cancelButton.style.visibility = 'visible';
  }
});
```

### getPrinters() and getPrinterInfo()

A single example is used for these functions because getting printer information requires a printer ID, which is retrieved by calling `getPrinters()`. This example logs the name and description of the default printer to the console. This is a simplified version of the printing example.

```javascript
const printers = await chrome.printing.getPrinters();
const defaultPrinter = printers.find(async (printer) => {
  const printerInfo = await chrome.printing.getPrinterInfo(printer.id);
  return printerInfo.isDefault;
});
if (defaultPrinter) {
    console.log(`Default printer: ${defaultPrinter.name}.\n\t${defaultPrinter.description}`);
}
```

### submitJob()

The `submitJob()` method requires three things.

*   A ticket structure specifying which capabilities of the printer are to be used. If the user needs to select from available capabilities, you can retrieve them for a specific printer using `getPrinterInfo()`.
*   A `SubmitJobRequest` structure, which specifies the printer to use, and the file or date to print. This structure contains a reference to the ticket structure.
*   A blob of the file or data to print.

Calling `submitJob()` triggers a dialog box asking the user to confirm printing. Use the `PrintingAPIExtensionsAllowlist` to bypass confirmation.

This is a simplified version of the printing example. Notice that the ticket is attached to the `SubmitJobRequest` structure (line 8) and that the data to print is converted to a blob (line 10). Getting the ID of the printer (line 1) is more complicated in the sample than is shown here.

```javascript
// Assuming getDefaultPrinter, getPrinterTicket, getPrintData are defined elsewhere
const defaultPrinterId = getDefaultPrinter(); 
const ticket = getPrinterTicket(defaultPrinterId); 
const arrayBuffer = getPrintData();

const submitJobRequest = {
  job: {
    printerId: defaultPrinterId, 
    title: 'test job',
    ticket: ticket,
    contentType: 'application/pdf',
    document: new Blob([new Uint8Array(arrayBuffer)], { type: 'application/pdf' })
  }
};

chrome.printing.submitJob(submitJobRequest, (response) => {
  if (response !== undefined) {
    console.log(response.status);
  }
  if (chrome.runtime.lastError !== undefined) {
    console.log(chrome.runtime.lastError.message);
  }
});
```

### Roll printing

This example shows how to build a printer ticket for continuous (or roll) printing, which is often used with receipt printing. The `submitJobRequest` object for roll printing is the same as that shown for the `submitJob()` example.

If you need to change the default value for paper cutting, use the `vendor_ticket_item` key. (The default varies from printer to printer.) To change the value, provide an array with one member: an object whose `id` is `'finishings'`. The `value` can either be `'trim'` for printers that cut the roll at the end of printing or `'none'` for printers that require the print job to be torn off.

```javascript
const ticket = {
  version: '1.0',
  print: {
    vendor_ticket_item: [{id: 'finishings', value: 'trim'}],
    color: {type: 'STANDARD_MONOCHROME'},
    duplex: {type: 'NO_DUPLEX'},
    page_orientation: {type: 'PORTRAIT'},
    copies: {copies: 1},
    dpi: {horizontal_dpi: 300, vertical_dpi: 300},
    media_size: {
      width_microns: 72320,
      height_microns: 100000
    },
    collate: {collate: false}
  }
};
```

Some printers do not support the `"finishings"` option. To determine if your printer does, call `getPrinterInfo()` and look for a `"display_name"` of `"finishings/11"`.

```json
"vendor_capability": [
  {
    "display_name": "finishings/11",
    "id": "finishings/11",
    "type": "TYPED_VALUE",
    "typed_value_cap": {
      "value_type": "BOOLEAN"
    }
  },
  ...
]
```

Note: starting with Chrome 124, the `vendor_ticket_item` allows all items from the printer's `vendor_capabilities`. For example, any value return by `getPrinterInfo()` is valid. Before, only the `finishings` key was supported.

The values in a ticket's `media_size` key are specific to each printer. To select an appropriate size call `getPrinterInfo()`. The returned `GetPrinterResponse` contains an array of supported media sizes at `"media_size"."option"`. Choose an option whose `"is_continuous_feed"` value is true. Use its height and width values for the ticket.

```json
"media_size": {
  "option": [
    {
      "custom_display_name": "",
      "is_continuous_feed": true,
      "max_height_microns": 2000000,
      "min_height_microns": 25400,
      "width_microns": 50800
    },
    ...
  ]
}
```

## Types

### GetPrinterInfoResponse

#### Properties

*   `capabilities`
    *   `object` optional
    *   Printer capabilities in CDD format. The property may be missing.
*   `status`
    *   `PrinterStatus`
    *   The status of the printer.

### JobStatus

Status of the print job.

#### Enum

*   `"PENDING"`: Print job is received on Chrome side but was not processed yet.
*   `"IN_PROGRESS"`: Print job is sent for printing.
*   `"FAILED"`: Print job was interrupted due to some error.
*   `"CANCELED"`: Print job was canceled by the user or via API.
*   `"PRINTED"`: Print job was printed without any errors.

### Printer

#### Properties

*   `description`
    *   `string`
    *   The human-readable description of the printer.
*   `id`
    *   `string`
    *   The printer's identifier; guaranteed to be unique among printers on the device.
*   `isDefault`
    *   `boolean`
    *   The flag which shows whether the printer fits `DefaultPrinterSelection` rules. Note that several printers could be flagged.
*   `name`
    *   `string`
    *   The name of the printer.
*   `recentlyUsedRank`
    *   `number` optional
    *   The value showing how recent the printer was used for printing from Chrome. The lower the value is the more recent the printer was used. The minimum value is `0`. Missing value indicates that the printer wasn't used recently. This value is guaranteed to be unique amongst printers.
*   `source`
    *   `PrinterSource`
    *   The source of the printer (user or policy configured).
*   `uri`
    *   `string`
    *   The printer URI. This can be used by extensions to choose the printer for the user.

### PrinterSource

The source of the printer.

#### Enum

*   `"USER"`: Printer was added by user.
*   `"POLICY"`: Printer was added via policy.

### PrinterStatus

The status of the printer.

#### Enum

*   `"DOOR_OPEN"`: The door of the printer is open. Printer still accepts print jobs.
*   `"TRAY_MISSING"`: The tray of the printer is missing. Printer still accepts print jobs.
*   `"OUT_OF_INK"`: The printer is out of ink. Printer still accepts print jobs.
*   `"OUT_OF_PAPER"`: The printer is out of paper. Printer still accepts print jobs.
*   `"OUTPUT_FULL"`: The output area of the printer (e.g. tray) is full. Printer still accepts print jobs.
*   `"PAPER_JAM"`: The printer has a paper jam. Printer still accepts print jobs.
*   `"GENERIC_ISSUE"`: Some generic issue. Printer still accepts print jobs.
*   `"STOPPED"`: The printer is stopped and doesn't print but still accepts print jobs.
*   `"UNREACHABLE"`: The printer is unreachable and doesn't accept print jobs.
*   `"EXPIRED_CERTIFICATE"`: The SSL certificate is expired. Printer accepts jobs but they fail.
*   `"AVAILABLE"`: The printer is available.

### SubmitJobRequest

#### Properties

*   `job`
    *   `PrintJob`
    *   The print job to be submitted. Supported content types are `"application/pdf"` and `"image/png"`. The Cloud Job Ticket shouldn't include `FitToPageTicketItem`, `PageRangeTicketItem` and `ReverseOrderTicketItem` fields since they are irrelevant for native printing. `VendorTicketItem` is optional. All other fields must be present.

### SubmitJobResponse

#### Properties

*   `jobId`
    *   `string` optional
    *   The id of created print job. This is a unique identifier among all print jobs on the device. If status is not `OK`, `jobId` will be `null`.
*   `status`
    *   `SubmitJobStatus`
    *   The status of the request.

### SubmitJobStatus

The status of `submitJob` request.

#### Enum

*   `"OK"`: Sent print job request is accepted.
*   `"USER_REJECTED"`: Sent print job request is rejected by the user.

## Properties

### MAX_GET_PRINTER_INFO_CALLS_PER_MINUTE

The maximum number of times that `getPrinterInfo` can be called per minute.

#### Value

`20`

### MAX_SUBMIT_JOB_CALLS_PER_MINUTE

The maximum number of times that `submitJob` can be called per minute.

#### Value

`40`

## Methods

### cancelJob()

`Promise`

```javascript
chrome.printing.cancelJob(
  jobId: string,
  callback?: function,
)
```

Cancels previously submitted job.

#### Parameters

*   `jobId`
    *   `string`
    *   The `id` of the print job to cancel. This should be the same `id` received in a `SubmitJobResponse`.
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        () => void
        ```

#### Returns

*   `Promise<void>`
    *   Chrome 100+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getJobStatus()

`Promise` Chrome 135+

```javascript
chrome.printing.getJobStatus(
  jobId: string,
  callback?: function,
)
```

Returns the status of the print job. This call will fail with a runtime error if the print job with the given `jobId` doesn't exist. `jobId`: The `id` of the print job to return the status of. This should be the same `id` received in a `SubmitJobResponse`.

#### Parameters

*   `jobId`
    *   `string`
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (status: JobStatus) => void
        ```
    *   `status`
        *   `JobStatus`

#### Returns

*   `Promise<JobStatus>`
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getPrinterInfo()

`Promise`

```javascript
chrome.printing.getPrinterInfo(
  printerId: string,
  callback?: function,
)
```

Returns the status and capabilities of the printer in CDD format. This call will fail with a runtime error if no printers with given `id` are installed.

#### Parameters

*   `printerId`
    *   `string`
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (response: GetPrinterInfoResponse) => void
        ```
    *   `response`
        *   `GetPrinterInfoResponse`

#### Returns

*   `Promise<GetPrinterInfoResponse>`
    *   Chrome 100+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getPrinters()

`Promise`

```javascript
chrome.printing.getPrinters(
  callback?: function,
)
```

Returns the list of available printers on the device. This includes manually added, enterprise and discovered printers.

#### Parameters

*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (printers: Printer[]) => void
        ```
    *   `printers`
        *   `Printer[]`

#### Returns

*   `Promise<Printer[]>`
    *   Chrome 100+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### submitJob()

`Promise`

```javascript
chrome.printing.submitJob(
  request: SubmitJobRequest,
  callback?: function,
)
```

Submits the job for printing. If the extension is not listed in the `PrintingAPIExtensionsAllowlist` policy, the user is prompted to accept the print job. Before Chrome 120, this function did not return a promise.

#### Parameters

*   `request`
    *   `SubmitJobRequest`
*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        (response: SubmitJobResponse) => void
        ```
    *   `response`
        *   `SubmitJobResponse`

#### Returns

*   `Promise<SubmitJobResponse>`
    *   Chrome 100+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onJobStatusChanged

```javascript
chrome.printing.onJobStatusChanged.addListener(
  callback: function,
)
```

Event fired when the status of the job is changed. This is only fired for the jobs created by this extension.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (jobId: string, status: JobStatus) => void
        ```
    *   `jobId`
        *   `string`
    *   `status`
        *   `JobStatus` 

===

---
title: chrome.printingMetrics
url: https://developer.chrome.com/docs/extensions/reference/api/printingMetrics
---

# `chrome.printingMetrics`

Important: This API works only on ChromeOS.

## Description

Use the `chrome.printingMetrics` API to fetch data about printing usage.

## Permissions

`printingMetrics`

## Availability

Chrome 79+ ChromeOS only Requires policy

## Types

### `ColorMode`

#### Enum

*   `"BLACK_AND_WHITE"`: Specifies that black and white mode was used.
*   `"COLOR"`: Specifies that color mode was used.

### `DuplexMode`

#### Enum

*   `"ONE_SIDED"`: Specifies that one-sided printing was used.
*   `"TWO_SIDED_LONG_EDGE"`: Specifies that two-sided printing was used, flipping on long edge.
*   `"TWO_SIDED_SHORT_EDGE"`: Specifies that two-sided printing was used, flipping on short edge.

### `MediaSize`

#### Properties

*   `height`: `number`

    Height (in micrometers) of the media used for printing.
*   `vendorId`: `string`

    Vendor-provided ID, e.g. `"iso_a3_297x420mm"` or `"na_index-3x5_3x5in"`. Possible values are values of `"media"` IPP attribute and can be found on [IANA page](https://www.iana.org/assignments/ipp-registrations/ipp-registrations.xhtml#ipp-registrations-media).
*   `width`: `number`

    Width (in micrometers) of the media used for printing.

### `Printer`

#### Properties

*   `name`: `string`

    Displayed name of the printer.
*   `source`: `PrinterSource`

    The source of the printer.
*   `uri`: `string`

    The full path for the printer. Contains protocol, hostname, port, and queue.

### `PrinterSource`

The source of the printer.

#### Enum

*   `"USER"`: Specifies that the printer was added by user.
*   `"POLICY"`: Specifies that the printer was added via policy.

### `PrintJobInfo`

#### Properties

*   `completionTime`: `number`

    The job completion time (in milliseconds past the Unix epoch).
*   `creationTime`: `number`

    The job creation time (in milliseconds past the Unix epoch).
*   `id`: `string`

    The ID of the job.
*   `numberOfPages`: `number`

    The number of pages in the document.
*   `printer`: `Printer`

    The info about the printer which printed the document.
*   `printer_status`: `PrinterStatus`

    Chrome 85+

    The status of the printer.
*   `settings`: `PrintSettings`

    The settings of the print job.
*   `source`: `PrintJobSource`

    Source showing who initiated the print job.
*   `sourceId`: `string optional`

    ID of source. Null if source is PRINT_PREVIEW or ANDROID_APP.
*   `status`: `PrintJobStatus`

    The final status of the job.
*   `title`: `string`

    The title of the document which was printed.

### `PrintJobSource`

The source of the print job.

#### Enum

*   `"PRINT_PREVIEW"`: Specifies that the job was created from the Print Preview page initiated by the user.
*   `"ANDROID_APP"`: Specifies that the job was created from an Android App.
*   `"EXTENSION"`: Specifies that the job was created by extension via Chrome API.
*   `"ISOLATED_WEB_APP"`: Specifies that the job was created by an Isolated Web App via API.

### `PrintJobStatus`

Specifies the final status of the print job.

#### Enum

*   `"FAILED"`: Specifies that the print job was interrupted due to some error.
*   `"CANCELED"`: Specifies that the print job was canceled by the user or via API.
*   `"PRINTED"`: Specifies that the print job was printed without any errors.

### `PrintSettings`

#### Properties

*   `color`: `ColorMode`

    The requested color mode.
*   `copies`: `number`

    The requested number of copies.
*   `duplex`: `DuplexMode`

    The requested duplex mode.
*   `mediaSize`: `MediaSize`

    The requested media size.

## Methods

### `getPrintJobs()`

`Promise`

```
chrome.printingMetrics.getPrintJobs( callback?: function, )
```

Returns the list of the finished print jobs.

#### Parameters

*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (jobs: PrintJobInfo[]) => void
    ```

    *   `jobs`: `PrintJobInfo[]`

#### Returns

*   `Promise<PrintJobInfo[]>`: Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onPrintJobFinished`

```
chrome.printingMetrics.onPrintJobFinished.addListener( callback: function, )
```

Event fired when the print job is finished. This includes any of termination statuses: FAILED, CANCELED and PRINTED.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (jobInfo: PrintJobInfo) => void
    ```

    *   `jobInfo`: `PrintJobInfo` 

===

---
title: chrome.privacy
url: https://developer.chrome.com/docs/extensions/reference/api/privacy
---

# `chrome.privacy`

Note: The [Chrome Privacy Whitepaper](https://www.google.com/chrome/browser/privacy/whitepaper.html) gives background detail regarding the features which this API can control.

## Description

Use the `chrome.privacy` API to control usage of the features in Chrome that can affect a user's privacy. This API relies on the `ChromeSetting` prototype of the [type](https://developer.chrome.com/docs/extensions/reference/api/types) API for getting and setting Chrome's configuration.

## Permissions

`privacy`

You must declare the `"privacy"` permission in your extension's manifest to use the API. For example:

```
{ "name": "My extension", ... "permissions": [ "privacy" ], ... }
```

## Concepts and usage

Reading the current value of a Chrome setting is straightforward. You'll first need to find the property you're interested in, then you'll call `get()` on that object in order to retrieve its current value and your extension's level of control. For example, to determine if Chrome's credit card autofill feature is enabled, you'd write:

```
chrome.privacy.services.autofillCreditCardEnabled.get({}, function(details) { if (details.value) { console.log('Autofill is on!'); } else { console.log('Autofill is off!'); } });
```

Changing the value of a setting is a little bit more complex, because you first must verify that your extension can control the setting. The user won't see any change to their settings if your extension toggles a setting that is either locked to a specific value by enterprise policies (`levelOfControl` will be set to `"not_controllable"`), or if another extension is controlling the value (`levelOfControl` will be set to `"controlled_by_other_extensions"`). The `set()` call will succeed, but the setting will be immediately overridden. As this might be confusing, it is advisable to warn the user when the settings they've chosen aren't practically applied.

Note: Full details about extensions' ability to control `ChromeSettings` can be found under `chrome.types.ChromeSetting`.

This means that you ought to use the `get()` method to determine your level of access, and then only call `set()` if your extension can grab control over the setting (in fact if your extension can't control the setting it's probably a good idea to visually disable the feature to reduce user confusion):

```
chrome.privacy.services.autofillCreditCardEnabled.get({}, function(details) { if (details.levelOfControl === 'controllable_by_this_extension') { chrome.privacy.services.autofillCreditCardEnabled.set({ value: true }, function() { if (chrome.runtime.lastError === undefined) { console.log("Hooray, it worked!"); } else { console.log("Sadness!", chrome.runtime.lastError); } }); } });
```

If you're interested in changes to a setting's value, add a listener to its `onChange` event. Among other uses, this will allow you to warn the user if a more recently installed extension grabs control of a setting, or if enterprise policy overrides your control. To listen for changes to credit card autofill status, for example, the following code would suffice:

```
chrome.privacy.services.autofillCreditCardEnabled.onChange.addListener( function (details) { // The new value is stored in `details.value`, the new level of control // in `details.levelOfControl`, and `details.incognitoSpecific` will be // `true` if the value is specific to Incognito mode. } );
```

## Examples

To try this API, install the [privacy API example](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api-samples/privacy) from the chrome-extension-samples repository.

## Types

### `IPHandlingPolicy`

Chrome 48+

The IP handling policy of WebRTC.

#### Enum

*   `"default"`
*   `"default_public_and_private_interfaces"`
*   `"default_public_interface_only"`
*   `"disable_non_proxied_udp"`

## Properties

### `network`

Settings that influence Chrome's handling of network connections in general.

#### Type

`object`

#### Properties

*   `networkPredictionEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome attempts to speed up your web browsing experience by pre-resolving DNS entries and preemptively opening TCP and SSL connections to servers. This preference only affects actions taken by Chrome's internal prediction service. It does not affect webpage-initiated prefectches or preconnects. This preference's value is a boolean, defaulting to true.
*   `webRTCIPHandlingPolicy`: `types.ChromeSetting<IPHandlingPolicy>`

    Chrome 48+

    Allow users to specify the media performance/privacy tradeoffs which impacts how WebRTC traffic will be routed and how much local address information is exposed. This preference's value is of type `IPHandlingPolicy`, defaulting to default.

### `services`

Settings that enable or disable features that require third-party network services provided by Google and your default search provider.

#### Type

`object`

#### Properties

*   `alternateErrorPagesEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome uses a web service to help resolve navigation errors. This preference's value is a boolean, defaulting to true.
*   `autofillAddressEnabled`: `types.ChromeSetting<boolean>`

    Chrome 70+

    If enabled, Chrome offers to automatically fill in addresses and other form data. This preference's value is a boolean, defaulting to true.
*   `autofillCreditCardEnabled`: `types.ChromeSetting<boolean>`

    Chrome 70+

    If enabled, Chrome offers to automatically fill in credit card forms. This preference's value is a boolean, defaulting to true.
*   `autofillEnabled`: `types.ChromeSetting<boolean>`

    Deprecated since Chrome 70

    Please use `privacy.services.autofillAddressEnabled` and `privacy.services.autofillCreditCardEnabled`. This remains for backward compatibility in this release and will be removed in the future.

    If enabled, Chrome offers to automatically fill in forms. This preference's value is a boolean, defaulting to true.
*   `passwordSavingEnabled`: `types.ChromeSetting<boolean>`

    If enabled, the password manager will ask if you want to save passwords. This preference's value is a boolean, defaulting to true.
*   `safeBrowsingEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome does its best to protect you from phishing and malware. This preference's value is a boolean, defaulting to true.
*   `safeBrowsingExtendedReportingEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome will send additional information to Google when SafeBrowsing blocks a page, such as the content of the blocked page. This preference's value is a boolean, defaulting to false.
*   `searchSuggestEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome sends the text you type into the Omnibox to your default search engine, which provides predictions of websites and searches that are likely completions of what you've typed so far. This preference's value is a boolean, defaulting to true.
*   `spellingServiceEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome uses a web service to help correct spelling errors. This preference's value is a boolean, defaulting to false.
*   `translationServiceEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome offers to translate pages that aren't in a language you read. This preference's value is a boolean, defaulting to true.

### `websites`

Settings that determine what information Chrome makes available to websites.

#### Type

`object`

#### Properties

*   `adMeasurementEnabled`: `types.ChromeSetting<boolean>`

    Chrome 111+

    If disabled, the Attribution Reporting API and Private Aggregation API are deactivated. The value of this preference is of type boolean, and the default value is true. Extensions may only disable these APIs by setting the value to false. If you try setting these APIs to true, it will throw an error.
*   `doNotTrackEnabled`: `types.ChromeSetting<boolean>`

    Chrome 65+

    If enabled, Chrome sends 'Do Not Track' (DNT: 1) header with your requests. The value of this preference is of type boolean, and the default value is false.
*   `fledgeEnabled`: `types.ChromeSetting<boolean>`

    Chrome 111+

    If disabled, the Fledge API is deactivated. The value of this preference is of type boolean, and the default value is true. Extensions may only disable this API by setting the value to false. If you try setting this API to true, it will throw an error.
*   `hyperlinkAuditingEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome sends auditing pings when requested by a website (`<a ping>`). The value of this preference is of type boolean, and the default value is true.
*   `protectedContentEnabled`: `types.ChromeSetting<boolean>`

    Available on Windows and ChromeOS only: If enabled, Chrome provides a unique ID to plugins in order to run protected content. The value of this preference is of type boolean, and the default value is true.
*   `referrersEnabled`: `types.ChromeSetting<boolean>`

    If enabled, Chrome sends referer headers with your requests. Yes, the name of this preference doesn't match the misspelled header. No, we're not going to change it. The value of this preference is of type boolean, and the default value is true.
*   `relatedWebsiteSetsEnabled`: `types.ChromeSetting<boolean>`

    Chrome 121+

    If disabled, Related Website Sets is deactivated. The value of this preference is of type boolean, and the default value is true. Extensions may only disable this API by setting the value to false. If you try setting this API to true, it will throw an error.
*   `thirdPartyCookiesAllowed`: `types.ChromeSetting<boolean>`

    If disabled, Chrome blocks third-party sites from setting cookies. The value of this preference is of type boolean, and the default value is true.

    \*\*Note:\*\*Individual sites may still be able to access third-party cookies when this API returns false, if they have a valid exemption or they use the Storage Access API instead.
*   `topicsEnabled`: `types.ChromeSetting<boolean>`

    Chrome 111+

    If disabled, the Topics API is deactivated. The value of this preference is of type boolean, and the default value is true. Extensions may only disable this API by setting the value to false. If you try setting this API to true, it will throw an error. 

===

---
title: chrome.processes
url: https://developer.chrome.com/docs/extensions/reference/api/processes
---

# `chrome.processes`

## Description

Use the `chrome.processes` API to interact with the browser's processes.

## Permissions

`processes`

## Availability

Dev channel

## Types

### `Cache`

#### Properties

*   `liveSize`: `number`

    The part of the cache that is utilized, in bytes.
*   `size`: `number`

    The size of the cache, in bytes.

### `Process`

#### Properties

*   `cpu`: `number optional`

    The most recent measurement of the process's CPU usage, expressed as the percentage of a single CPU core used in total, by all of the process's threads. This gives a value from zero to `CpuInfo.numOfProcessors`\*100, which can exceed 100% in multi-threaded processes. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `cssCache`: `Cache optional`

    The most recent information about the CSS cache for the process. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `id`: `number`

    Unique ID of the process provided by the browser.
*   `imageCache`: `Cache optional`

    The most recent information about the image cache for the process. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `jsMemoryAllocated`: `number optional`

    The most recent measurement of the process JavaScript allocated memory, in bytes. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `jsMemoryUsed`: `number optional`

    The most recent measurement of the process JavaScript memory used, in bytes. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `naclDebugPort`: `number`

    The debugging port for Native Client processes. Zero for other process types and for NaCl processes that do not have debugging enabled.
*   `network`: `number optional`

    The most recent measurement of the process network usage, in bytes per second. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `osProcessId`: `number`

    The ID of the process, as provided by the OS.
*   `privateMemory`: `number optional`

    The most recent measurement of the process private memory usage, in bytes. Only available when receiving the object as part of a callback from `onUpdatedWithMemory` or `getProcessInfo` with the includeMemory flag.
*   `profile`: `string`

    The profile which the process is associated with.
*   `scriptCache`: `Cache optional`

    The most recent information about the script cache for the process. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `sqliteMemory`: `number optional`

    The most recent measurement of the process's SQLite memory usage, in bytes. Only available when receiving the object as part of a callback from `onUpdated` or `onUpdatedWithMemory`.
*   `tasks`: `TaskInfo[]`

    Array of TaskInfos representing the tasks running on this process.
*   `type`: `ProcessType`

    The type of process.

### `ProcessType`

The types of the browser processes.

#### Enum

*   `"browser"`
*   `"renderer"`
*   `"extension"`
*   `"notification"`
*   `"plugin"`
*   `"worker"`
*   `"nacl"`
*   `"service_worker"`
*   `"utility"`
*   `"gpu"`
*   `"other"`

### `TaskInfo`

#### Properties

*   `tabId`: `number optional`

    Optional tab ID, if this task represents a tab running on a renderer process.
*   `title`: `string`

    The title of the task.

## Methods

### `getProcessIdForTab()`

`Promise`

```
chrome.processes.getProcessIdForTab( tabId: number, callback?: function, )
```

Returns the ID of the renderer process for the specified tab.

#### Parameters

*   `tabId`: `number`

    The ID of the tab for which the renderer process ID is to be returned.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (processId: number) => void
    ```

    *   `processId`: `number`

        Process ID of the tab's renderer process.

#### Returns

*   `Promise<number>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getProcessInfo()`

`Promise`

```
chrome.processes.getProcessInfo( processIds: number | number[], includeMemory: boolean, callback?: function, )
```

Retrieves the process information for each process ID specified.

#### Parameters

*   `processIds`: `number | number[]`

    The list of process IDs or single process ID for which to return the process information. An empty list indicates all processes are requested.
*   `includeMemory`: `boolean`

    True if detailed memory usage is required. Note, collecting memory usage information incurs extra CPU usage and should only be queried for when needed.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (processes: object) => void
    ```

    *   `processes`: `object`

        A dictionary of `Process` objects for each requested process that is a live child process of the current browser process, indexed by process ID. Metrics requiring aggregation over time will not be populated in each Process object.

#### Returns

*   `Promise<object>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `terminate()`

`Promise`

```
chrome.processes.terminate( processId: number, callback?: function, )
```

Terminates the specified renderer process. Equivalent to visiting about:crash, but without changing the tab's URL.

#### Parameters

*   `processId`: `number`

    The ID of the process to be terminated.
*   `callback`: `function optional`

    The callback parameter looks like:

    ```
    (didTerminate: boolean) => void
    ```

    *   `didTerminate`: `boolean`

        True if terminating the process was successful, and false otherwise.

#### Returns

*   `Promise<boolean>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onCreated`

```
chrome.processes.onCreated.addListener( callback: function, )
```

Fired each time a process is created, providing the corrseponding `Process` object.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (process: Process) => void
    ```

    *   `process`: `Process`

### `onExited`

```
chrome.processes.onExited.addListener( callback: function, )
```

Fired each time a process is terminated, providing the type of exit.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (processId: number, exitType: number, exitCode: number) => void
    ```

    *   `processId`: `number`
    *   `exitType`: `number`
    *   `exitCode`: `number`

### `onUnresponsive`

```
chrome.processes.onUnresponsive.addListener( callback: function, )
```

Fired each time a process becomes unresponsive, providing the corrseponding `Process` object.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (process: Process) => void
    ```

    *   `process`: `Process`

### `onUpdated`

```
chrome.processes.onUpdated.addListener( callback: function, )
```

Fired each time the Task Manager updates its process statistics, providing the dictionary of updated `Process` objects, indexed by process ID.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (processes: object) => void
    ```

    *   `processes`: `object`

### `onUpdatedWithMemory`

```
chrome.processes.onUpdatedWithMemory.addListener( callback: function, )
```

Fired each time the Task Manager updates its process statistics, providing the dictionary of updated `Process` objects, indexed by process ID. Identical to onUpdate, with the addition of memory usage details included in each `Process` object. Note, collecting memory usage information incurs extra CPU usage and should only be listened for when needed.

#### Parameters

*   `callback`: `function`

    The callback parameter looks like:

    ```
    (processes: object) => void
    ```

    *   `processes`: `object` 

===

---
title: chrome.proxy
url: https://developer.chrome.com/docs/extensions/reference/api/proxy
---

# chrome.proxy

## Description

Use the `chrome.proxy` API to manage Chrome's proxy settings. This API relies on the `ChromeSetting` prototype of the type API for getting and setting the proxy configuration.

## Permissions

`proxy`

You must declare the "proxy" permission in the extension manifest to use the proxy settings API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "proxy"
  ],
  ...
}
```

## Concepts and usage

Proxy settings are defined in a `proxy.ProxyConfig` object. Depending on Chrome's proxy settings, the settings may contain `proxy.ProxyRules` or a `proxy.PacScript`.

### Proxy modes

A `ProxyConfig` object's `mode` attribute determines the overall behavior of Chrome with regards to proxy usage. It can take the following values:

`direct`
:   In `direct` mode all connections are created directly, without any proxy involved. This mode allows no further parameters in the `ProxyConfig` object.

`auto_detect`
:   In `auto_detect` mode the proxy configuration is determined by a PAC script that can be downloaded at `http://wpad/wpad.dat`. This mode allows no further parameters in the `ProxyConfig` object.

`pac_script`
:   In `pac_script` mode the proxy configuration is determined by a PAC script that is either retrieved from the URL specified in the `proxy.PacScript` object or taken literally from the `data` element specified in the `proxy.PacScript` object. Besides this, this mode allows no further parameters in the `ProxyConfig` object.

`fixed_servers`
:   In `fixed_servers` mode the proxy configuration is codified in a `proxy.ProxyRules` object. Its structure is described in Proxy rules. Besides this, the `fixed_servers` mode allows no further parameters in the `ProxyConfig` object.

`system`
:   In `system` mode the proxy configuration is taken from the operating system. This mode allows no further parameters in the `ProxyConfig` object. Note that the `system` mode is different from setting no proxy configuration. In the latter case, Chrome falls back to the system settings only if no command-line options influence the proxy configuration.

### Proxy rules

The `proxy.ProxyRules` object can contain either a `singleProxy` attribute or a subset of `proxyForHttp`, `proxyForHttps`, `proxyForFtp`, and `fallbackProxy`.

In the first case, HTTP, HTTPS and FTP traffic is proxied through the specified proxy server. Other traffic is sent directly. In the latter case the behavior is slightly more subtle: If a proxy server is configured for the HTTP, HTTPS or FTP protocol, the respective traffic is proxied through the specified server. If no such proxy server is specified or traffic uses a different protocol than HTTP, HTTPS or FTP, the `fallbackProxy` is used. If no `fallbackProxy` is specified, traffic is sent directly without a proxy server.

### Proxy server objects

A proxy server is configured in a `proxy.ProxyServer` object. The connection to the proxy server (defined by the `host` attribute) uses the protocol defined in the `scheme` attribute. If no `scheme` is specified, the proxy connection defaults to `http`.

If no `port` is defined in a `proxy.ProxyServer` object, the `port` is derived from the `scheme`. The default ports are:

| Scheme  | Port   |
| ------- | ------ |
| `http`  | 80     |
| `https` | 443    |
| `socks4`| 1080   |
| `socks5`| 1080   |

### Bypass list

Individual servers may be excluded from being proxied with the `bypassList`. This list may contain the following entries:

`[SCHEME://]HOST_PATTERN[:PORT]`
:   Match all hostnames that match the pattern `HOST_PATTERN`. A leading "." is interpreted as a "\*.".

    Examples: "foobar.com", "\*foobar.com", "\*.foobar.com", "\*foobar.com:99", "https://x.\*.y.com:99".

    | Pattern         | Matches                                       | Does not match |
    | --------------- | --------------------------------------------- | -------------- |
    | ".foobar.com"   | "www.foobar.com"                              | "foobar.com"   |
    | "\*.foobar.com" | "www.foobar.com"                              | "foobar.com"   |
    | "foobar.com"    | "foobar.com"                                  | "www.foobar.com" |
    | "\*foobar.com"  | "foobar.com", "www.foobar.com", "foofoobar.com" |                |

`[SCHEME://]IP_LITERAL[:PORT]`
:   Match URLs that are IP address literals. Conceptually this is the similar to the first case, but with special cases to handle IP literal canonicalization. For example, matching on "[0:0:0::1]" is the same as matching on "[::1]" because the IPv6 canonicalization is done internally.

    Examples: `127.0.1`, `[0:0::1]`, `[::1]:80`, `https://[::1]:443`

`IP_LITERAL/PREFIX_LENGTH_IN_BITS`
:   Match any URL containing an IP literal (`IP_LITERAL`) within the given range. The IP range (`PREFIX_LENGTH_IN_BITS`) is specified using CIDR notation.
:   Match any URL containing an IP literal within the given range. The IP range is specified using CIDR notation. Examples: "192.168.1.1/16", "fefe:13::abc/33"

`<local>`
:   The literal string `<local>` matches simple hostnames. A simple hostname is one that contains no dots and is not an IP literal. For instance `example` and `localhost` are simple hostnames, whereas `example.com`, `example.`, and `[::1]` are not.

    Example: "`<local>`"

## Examples

The following code sets a SOCKS 5 proxy for HTTP connections to all servers but `foobar.com` and uses direct connections for all other protocols. The settings apply to regular and incognito windows, as incognito windows inherit settings from regular windows. See also the Types API documentation.

```javascript
var config = {
  mode: "fixed_servers",
  rules: {
    proxyForHttp: {
      scheme: "socks5",
      host: "1.2.3.4"
    },
    bypassList: ["foobar.com"]
  }
};
chrome.proxy.settings.set(
  {value: config, scope: 'regular'},
  function() {});
```

The following code sets a custom PAC script.

```javascript
var config = {
  mode: "pac_script",
  pacScript: {
    data: "function FindProxyForURL(url, host) {\n" +
          "  if (host == 'foobar.com')\n" +
          "    return 'PROXY blackhole:80';\n" +
          "  return 'DIRECT';\n" +
          "}"
  }
};
chrome.proxy.settings.set(
  {value: config, scope: 'regular'},
  function() {});
```

The next snippet queries the current effective proxy settings. The effective proxy settings can be determined by another extension or by a policy. See the Types API documentation for details.

```javascript
chrome.proxy.settings.get(
  {'incognito': false},
  function(config) {
    console.log(JSON.stringify(config));
  });
```

Note that the `value` object passed to `set()` is not identical to the `value` object passed to callback function of `get()`. The latter will contain a `rules.proxyForHttp.port` element.

## Types

### Mode

Chrome 54+

#### Enum

"direct"

"auto_detect"

"pac_script"

"fixed_servers"

"system"

### PacScript

An object holding proxy auto-config information. Exactly one of the fields should be non-empty.

#### Properties

*   `data`
    string optional
    A PAC script.
*   `mandatory`
    boolean optional
    If `true`, an invalid PAC script will prevent the network stack from falling back to direct connections. Defaults to `false`.
*   `url`
    string optional
    URL of the PAC file to be used.

### ProxyConfig

An object encapsulating a complete proxy configuration.

#### Properties

*   `mode`
    `Mode`
    `'direct'` = Never use a proxy
    `'auto_detect'` = Auto detect proxy settings
    `'pac_script'` = Use specified PAC script
    `'fixed_servers'` = Manually specify proxy servers
    `'system'` = Use system proxy settings
*   `pacScript`
    `PacScript` optional
    The proxy auto-config (PAC) script for this configuration. Use this for `'pac_script'` mode.
*   `rules`
    `ProxyRules` optional
    The proxy rules describing this configuration. Use this for `'fixed_servers'` mode.

### ProxyRules

An object encapsulating the set of proxy rules for all protocols. Use either `'singleProxy'` or (a subset of) `'proxyForHttp'`, `'proxyForHttps'`, `'proxyForFtp'` and `'fallbackProxy'`.

#### Properties

*   `bypassList`
    string[] optional
    List of servers to connect to without a proxy server.
*   `fallbackProxy`
    `ProxyServer` optional
    The proxy server to be used for everthing else or if any of the specific `proxyFor...` is not specified.
*   `proxyForFtp`
    `ProxyServer` optional
    The proxy server to be used for FTP requests.
*   `proxyForHttp`
    `ProxyServer` optional
    The proxy server to be used for HTTP requests.
*   `proxyForHttps`
    `ProxyServer` optional
    The proxy server to be used for HTTPS requests.
*   `singleProxy`
    `ProxyServer` optional
    The proxy server to be used for all per-URL requests (that is `http`, `https`, and `ftp`).

### ProxyServer

An object encapsulating a single proxy server's specification.

#### Properties

*   `host`
    string
    The hostname or IP address of the proxy server. Hostnames must be in ASCII (in Punycode format). IDNA is not supported, yet.
*   `port`
    number optional
    The port of the proxy server. Defaults to a port that depends on the scheme.
*   `scheme`
    `Scheme` optional
    The scheme (protocol) of the proxy server itself. Defaults to `'http'`.

### Scheme

Chrome 54+

#### Enum

"http"

"https"

"quic"

"socks4"

"socks5"

## Properties

### settings

Proxy settings to be used. The value of this setting is a `ProxyConfig` object.

#### Type

`types.ChromeSetting<ProxyConfig>`

## Events

### onProxyError

```
chrome.proxy.onProxyError.addListener(
  callback: function,
)
```

Notifies about proxy errors.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (details: object) => void
    ```
    *   `details`
        object
        *   `details`
            string
            Additional details about the error such as a JavaScript runtime error.
        *   `error`
            string
            The error description.
        *   `fatal`
            boolean
            If `true`, the error was fatal and the network transaction was aborted. Otherwise, a direct connection is used instead. 

===

---
title: chrome.readingList
url: https://developer.chrome.com/docs/extensions/reference/api/readingList
---

# chrome.readingList

## Description

Use the `chrome.readingList` API to read from and modify the items in the Reading List.

## Permissions

`readingList`

To use the Reading List API, add the "readingList" permission in the extension manifest file:

manifest.json:

```json
{
  "name": "My reading list extension",
  ...
  "permissions": [
    "readingList"
  ]
}
```

## Availability

Chrome 120+ MV3+

Chrome features a reading list located on the side panel. It lets users save web pages to read later or when offline. Use the Reading List API to retrieve existing items and add or remove items from the list.

Reading list showing a number of articles

## Concepts and usage

### Item ordering

Items in the reading list are not in any guaranteed order.

### Item uniqueness

Items are keyed by URL. This includes the hash and query string.

## Use cases

The following sections demonstrate some common use cases for the Reading List API. See Extension samples for complete extension examples.

### Add an item

To add an item to the reading list, use `chrome.readingList.addEntry()`:

```javascript
chrome.readingList.addEntry({
  title: "New to the web platform in September | web.dev",
  url: "https://developer.chrome.com/",
  hasBeenRead: false
});
```

### Display items

To display items from the reading list, use the `chrome.readingList.query()` method to retrieve them. method.

```javascript
const items = await chrome.readingList.query({});
for (const item of items) {
  // Do something do display the item
}
```

### Mark an item as read

You can use `chrome.readingList.updateEntry()` to update the title, URL, and read status. The following code marks an item as read:

```javascript
chrome.readingList.updateEntry({
  url: "https://developer.chrome.com/",
  hasBeenRead: true
});
```

### Remove an item

To remove an item, use `chrome.readingList.removeEntry()`:

```javascript
chrome.readingList.removeEntry({ url: "https://developer.chrome.com/" });
```

## Extension samples

For more Reading List API extensions demos, see the Reading List API sample.

## Types

### AddEntryOptions

#### Properties

*   `hasBeenRead`
    boolean
    Will be `true` if the entry has been read.
*   `title`
    string
    The title of the entry.
*   `url`
    string
    The url of the entry.

### QueryInfo

#### Properties

*   `hasBeenRead`
    boolean optional
    Indicates whether to search for read (`true`) or unread (`false`) items.
*   `title`
    string optional
    A title to search for.
*   `url`
    string optional
    A url to search for.

### ReadingListEntry

#### Properties

*   `creationTime`
    number
    The time the entry was created. Recorded in milliseconds since Jan 1, 1970.
*   `hasBeenRead`
    boolean
    Will be `true` if the entry has been read.
*   `lastUpdateTime`
    number
    The last time the entry was updated. This value is in milliseconds since Jan 1, 1970.
*   `title`
    string
    The title of the entry.
*   `url`
    string
    The url of the entry.

### RemoveOptions

#### Properties

*   `url`
    string
    The url to remove.

### UpdateEntryOptions

#### Properties

*   `hasBeenRead`
    boolean optional
    The updated read status. The existing status remains if a value isn't provided.
*   `title`
    string optional
    The new title. The existing tile remains if a value isn't provided.
*   `url`
    string
    The url that will be updated.

## Methods

### addEntry()

Promise

```
chrome.readingList.addEntry(
  entry: AddEntryOptions,
  callback?: function,
)
```

Adds an entry to the reading list if it does not exist.

#### Parameters

*   `entry`
    `AddEntryOptions`
    The entry to add to the reading list.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### query()

Promise

```
chrome.readingList.query(
  info: QueryInfo,
  callback?: function,
)
```

Retrieves all entries that match the `QueryInfo` properties. Properties that are not provided will not be matched.

#### Parameters

*   `info`
    `QueryInfo`
    The properties to search for.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (entries: ReadingListEntry[]) => void
    ```
    *   `entries`
        `ReadingListEntry`[]

#### Returns

*   Promise&lt;`ReadingListEntry`[]&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeEntry()

Promise

```
chrome.readingList.removeEntry(
  info: RemoveOptions,
  callback?: function,
)
```

Removes an entry from the reading list if it exists.

#### Parameters

*   `info`
    `RemoveOptions`
    The entry to remove from the reading list.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### updateEntry()

Promise

```
chrome.readingList.updateEntry(
  info: UpdateEntryOptions,
  callback?: function,
)
```

Updates a reading list entry if it exists.

#### Parameters

*   `info`
    `UpdateEntryOptions`
    The entry to update.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onEntryAdded

```
chrome.readingList.onEntryAdded.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is added to the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry`

### onEntryRemoved

```
chrome.readingList.onEntryRemoved.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is removed from the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry`

### onEntryUpdated

```
chrome.readingList.onEntryUpdated.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is updated in the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry` 

===

---
title: chrome.runtime
url: https://developer.chrome.com/docs/extensions/reference/runtime
---

## Description

Use the `chrome.runtime` API to retrieve the service worker, return details about the manifest, and listen for and respond to events in the extension lifecycle. You can also use this API to convert the relative path of URLs to fully-qualified URLs.

Most members of this API do not require any permissions. This permission is needed for `connectNative()`, `sendNativeMessage()` and `onNativeConnect`.

The following example shows how to declare the "nativeMessaging" permission in the manifest:

`manifest.json`:

```
{
  "name": "My extension",
  ...
  "permissions": [
    "nativeMessaging"
  ],
  ...
}
```

## Concepts and usage

The Runtime API provides methods to support a number of areas that your extensions can use:

Message passing
: Your extension can communicate with different contexts within your extension and also with other extensions using these methods and events: `connect()`, `onConnect`, `onConnectExternal`, `sendMessage()`, `onMessage` and `onMessageExternal`. In addition, your extension can pass messages to native applications on the user's device using `connectNative()` and `sendNativeMessage()`.

Note: See Message Passing for an overview of the subject.

Accessing extension and platform metadata
: These methods let you retrieve several specific pieces of metadata about the extension and the platform. Methods in this category include `getManifest()`, and `getPlatformInfo()`.

Managing extension lifecycle and options
: These properties let you perform some meta-operations on the extension, and display the options page. Methods and events in this category include `onInstalled`, `onStartup`, `openOptionsPage()`, `reload()`, `requestUpdateCheck()`, and `setUninstallURL()`.

Helper utilities
: These methods provide utility such as the conversion of internal resource representations to external formats. Methods in this category include `getURL()`.

Kiosk mode utilities
: These methods are available only on ChromeOS, and exist mainly to support kiosk implementations. Methods in this category include `restart()` and `restartAfterDelay()`.

### Unpacked extension behavior

When an unpacked extension is reloaded, this is treated as an update. This means that the `chrome.runtime.onInstalled` event will fire with the "update" reason. This includes when the extension is reloaded with `chrome.runtime.reload()`.

## Use cases

### Add an image to a web page

For a web page to access an asset hosted on another domain, it must specify the resource's full URL (e.g. `<img src="https://example.com/logo.png">`). The same is true to include an extension asset on a web page. The two differences are that the extension's assets must be exposed as web accessible resources and that typically content scripts are responsible for injecting extension assets.

In this example, the extension will add `logo.png` to the page that the content script is being injected into by using `runtime.getURL()` to create a fully-qualified URL. But first, the asset must be declared as a web accessible resource in the manifest.

`manifest.json`:

```
{
  ...
  "web_accessible_resources": [
    {
      "resources": [
        "logo.png"
      ],
      "matches": [
        "https://*/*"
      ]
    }
  ],
  ...
}
```

`content.js`:

```
{
  // Block used to avoid setting global variables
  const img = document.createElement('img');
  img.src = chrome.runtime.getURL('logo.png');
  document.body.append(img);
}
```

### Send data from a content script to the service worker

Its common for an extension's content scripts to need data managed by another part of the extension, like the service worker. Much like two browser windows opened to the same web page, these two contexts cannot directly access each other's values. Instead, the extension can use message passing to coordinate across these different contexts.

In this example, the content script needs some data from the extension's service worker to initialize its UI. To get this data, it passes the developer-defined `get-user-data` message to the service worker, and it responds with a copy of the user's information.

`content.js`:

```
// 1. Send a message to the service worker requesting the user's data
chrome.runtime.sendMessage('get-user-data', (response) => {
  // 3. Got an asynchronous response with the data from the service worker
  console.log('received user data', response);
  initializeUI(response);
});
```

`service-worker.js`:

```
// Example of a simple user data object
const user = {
  username: 'demo-user'
};
chrome.runtime.onMessage.addListener((message, sender, sendResponse) => {
  // 2. A page requested user data, respond with a copy of `user`
  if (message === 'get-user-data') {
    sendResponse(user);
  }
});
```

### Gather feedback on uninstall

Many extensions use post-uninstall surveys to understand how the extension could better serve its users and improve retention. The following example shows how to add this functionality.

`background.js`:

```
chrome.runtime.onInstalled.addListener(details => {
  if (details.reason === chrome.runtime.OnInstalledReason.INSTALL) {
    chrome.runtime.setUninstallURL('https://example.com/extension-survey');
  }
});
```

## Examples

See the Manifest V3 - Web Accessible Resources demo for more Runtime API examples.

## Types

### ContextFilter

Chrome 114+

A filter to match against certain extension contexts. Matching contexts must match all specified filters; any filter that is not specified matches all available contexts. Thus, a filter of `{}` will match all available contexts.

#### Properties

* `contextIds`

  `string[]` optional
* `contextTypes`

  `ContextType[]` optional
* `documentIds`

  `string[]` optional
* `documentOrigins`

  `string[]` optional
* `documentUrls`

  `string[]` optional
* `frameIds`

  `number[]` optional
* `incognito`

  `boolean` optional
* `tabIds`

  `number[]` optional
* `windowIds`

  `number[]` optional

### ContextType

Chrome 114+

#### Enum

`"TAB"` Specifies the context type as a tab

`"POPUP"` Specifies the context type as an extension popup window

`"BACKGROUND"` Specifies the context type as a service worker.

`"OFFSCREEN_DOCUMENT"` Specifies the context type as an offscreen document.

`"SIDE_PANEL"` Specifies the context type as a side panel.

`"DEVELOPER_TOOLS"` Specifies the context type as developer tools.

### ExtensionContext

Chrome 114+

A context hosting extension content.

#### Properties

* `contextId`

  `string`

  A unique identifier for this context
* `contextType`

  `ContextType`

  The type of context this corresponds to.
* `documentId`

  `string` optional

  A UUID for the document associated with this context, or undefined if this context is hosted not in a document.
* `documentOrigin`

  `string` optional

  The origin of the document associated with this context, or undefined if the context is not hosted in a document.
* `documentUrl`

  `string` optional

  The URL of the document associated with this context, or undefined if the context is not hosted in a document.
* `frameId`

  `number`

  The ID of the frame for this context, or -1 if this context is not hosted in a frame.
* `incognito`

  `boolean`

  Whether the context is associated with an incognito profile.
* `tabId`

  `number`

  The ID of the tab for this context, or -1 if this context is not hosted in a tab.
* `windowId`

  `number`

  The ID of the window for this context, or -1 if this context is not hosted in a window.

### MessageSender

An object containing information about the script context that sent a message or request.

#### Properties

* `documentId`

  `string` optional

  Chrome 106+

  A UUID of the document that opened the connection.
* `documentLifecycle`

  `string` optional

  Chrome 106+

  The lifecycle the document that opened the connection is in at the time the port was created. Note that the lifecycle state of the document may have changed since port creation.
* `frameId`

  `number` optional

  The frame that opened the connection. 0 for top-level frames, positive for child frames. This will only be set when tab is set.
* `id`

  `string` optional

  The ID of the extension that opened the connection, if any.
* `nativeApplication`

  `string` optional

  Chrome 74+

  The name of the native application that opened the connection, if any.
* `origin`

  `string` optional

  Chrome 80+

  The origin of the page or frame that opened the connection. It can vary from the url property (e.g., about:blank) or can be opaque (e.g., sandboxed iframes). This is useful for identifying if the origin can be trusted if we can't immediately tell from the URL.
* `tab`

  `Tab` optional

  The `tabs.Tab` which opened the connection, if any. This property will only be present when the connection was opened from a tab (including content scripts), and only if the receiver is an extension, not an app.
* `tlsChannelId`

  `string` optional

  The TLS channel ID of the page or frame that opened the connection, if requested by the extension, and if available.
* `url`

  `string` optional

  The URL of the page or frame that opened the connection. If the sender is in an iframe, it will be iframe's URL not the URL of the page which hosts it.

### OnInstalledReason

Chrome 44+

The reason that this event is being dispatched.

#### Enum

`"install"` Specifies the event reason as an installation.

`"update"` Specifies the event reason as an extension update.

`"chrome_update"` Specifies the event reason as a Chrome update.

`"shared_module_update"` Specifies the event reason as an update to a shared module.

### OnRestartRequiredReason

Chrome 44+

The reason that the event is being dispatched. `'app_update'` is used when the restart is needed because the application is updated to a newer version. `'os_update'` is used when the restart is needed because the browser/OS is updated to a newer version. `'periodic'` is used when the system runs for more than the permitted uptime set in the enterprise policy.

#### Enum

`"app_update"` Specifies the event reason as an update to the app.

`"os_update"` Specifies the event reason as an update to the operating system.

`"periodic"` Specifies the event reason as a periodic restart of the app.

### PlatformArch

Chrome 44+

The machine's processor architecture.

#### Enum

`"arm"` Specifies the processer architecture as arm.

`"arm64"` Specifies the processer architecture as arm64.

`"x86-32"` Specifies the processer architecture as x86-32.

`"x86-64"` Specifies the processer architecture as x86-64.

`"mips"` Specifies the processer architecture as mips.

`"mips64"` Specifies the processer architecture as mips64.

### PlatformInfo

An object containing information about the current platform.

#### Properties

* `arch`

  `PlatformArch`

  The machine's processor architecture.
* `nacl_arch`

  `PlatformNaclArch`

  The native client architecture. This may be different from arch on some platforms.
* `os`

  `PlatformOs`

  The operating system Chrome is running on.

### PlatformNaclArch

Chrome 44+

The native client architecture. This may be different from arch on some platforms.

#### Enum

`"arm"` Specifies the native client architecture as arm.

`"x86-32"` Specifies the native client architecture as x86-32.

`"x86-64"` Specifies the native client architecture as x86-64.

`"mips"` Specifies the native client architecture as mips.

`"mips64"` Specifies the native client architecture as mips64.

### PlatformOs

Chrome 44+

The operating system Chrome is running on.

#### Enum

`"mac"` Specifies the MacOS operating system.

`"win"` Specifies the Windows operating system.

`"android"` Specifies the Android operating system.

`"cros"` Specifies the Chrome operating system.

`"linux"` Specifies the Linux operating system.

`"openbsd"` Specifies the OpenBSD operating system.

`"fuchsia"` Specifies the Fuchsia operating system.

### Port

An object which allows two way communication with other pages. See Long-lived connections for more information.

#### Properties

* `name`

  `string`

  The name of the port, as specified in the call to `runtime.connect`.
* `onDisconnect`

  `Event<functionvoidvoid>`

  Fired when the port is disconnected from the other end(s). `runtime.lastError` may be set if the port was disconnected by an error. If the port is closed via `disconnect`, then this event is only fired on the other end. This event is fired at most once (see also Port lifetime).

  The `onDisconnect.addListener` function looks like:

  ```
  (callback: function) => {...}
  ```

  + `callback`

    `function`

    The callback parameter looks like:

    ```
    (port: Port) => void
    ```

    - `port`

      `Port`
* `onMessage`

  `Event<functionvoidvoid>`

  This event is fired when `postMessage` is called by the other end of the port.

  The `onMessage.addListener` function looks like:

  ```
  (callback: function) => {...}
  ```

  + `callback`

    `function`

    The callback parameter looks like:

    ```
    (message: any, port: Port) => void
    ```

    - `message`

      `any`
    - `port`

      `Port`
* `sender`

  `MessageSender` optional

  This property will only be present on ports passed to `onConnect` / `onConnectExternal` / `onConnectNative` listeners.
* `disconnect`

  `void`

  Immediately disconnect the port. Calling `disconnect()` on an already-disconnected port has no effect. When a port is disconnected, no new events will be dispatched to this port.

  The `disconnect` function looks like:

  ```
  () => {...}
  ```
* `postMessage`

  `void`

  Send a message to the other end of the port. If the port is disconnected, an error is thrown.

  The `postMessage` function looks like:

  ```
  (message: any) => {...}
  ```

  + `message`

    `any`

    Chrome 52+

    The message to send. This object should be JSON-ifiable.

## Properties

### id

The ID of the extension/app.

#### Type

`string`

### lastError

Populated with an error message if calling an API function fails; otherwise undefined. This is only defined within the scope of that function's callback. If an error is produced, but `runtime.lastError` is not accessed within the callback, a message is logged to the console listing the API function that produced the error. API functions that return promises do not set this property.

#### Type

`object`

#### Properties

* `message`

  `string` optional

  Details about the error which occurred.

## Methods

### connect()

```
chrome.runtime.connect( extensionId?: string, connectInfo?: object, )
```

Attempts to connect listeners within an extension (such as the background page), or other extensions/apps. This is useful for content scripts connecting to their extension processes, inter-app/extension communication, and web messaging. Note that this does not connect to any listeners in a content script. Extensions may connect to content scripts embedded in tabs via `tabs.connect`.

#### Parameters

* `extensionId`

  `string` optional

  The ID of the extension to connect to. If omitted, a connection will be attempted with your own extension. Required if sending messages from a web page for web messaging.
* `connectInfo`

  `object` optional

  + `includeTlsChannelId`

    `boolean` optional

    Whether the TLS channel ID will be passed into `onConnectExternal` for processes that are listening for the connection event.
  + `name`

    `string` optional

    Will be passed into `onConnect` for processes that are listening for the connection event.

#### Returns

* `Port`

  `Port` through which messages can be sent and received. The port's `onDisconnect` event is fired if the extension does not exist.

### connectNative()

```
chrome.runtime.connectNative( application: string, )
```

Connects to a native application in the host machine. This method requires the "nativeMessaging" permission. See Native Messaging for more information.

#### Parameters

* `application`

  `string`

  The name of the registered application to connect to.

#### Returns

* `Port`

  `Port` through which messages can be sent and received with the application

### getBackgroundPage()

Promise Foreground only Deprecated since Chrome 133

```
chrome.runtime.getBackgroundPage( callback?: function, )
```

Background pages do not exist in MV3 extensions.

Retrieves the JavaScript 'window' object for the background page running inside the current extension/app. If the background page is an event page, the system will ensure it is loaded before calling the callback. If there is no background page, an error is set.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (backgroundPage?: Window) => void
  ```

  + `backgroundPage`

    `Window` optional

    The JavaScript 'window' object for the background page.

#### Returns

* `Promise<Window | undefined>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getContexts()

Promise Chrome 116+ MV3+

```
chrome.runtime.getContexts( filter: ContextFilter, callback?: function, )
```

Fetches information about active contexts associated with this extension

#### Parameters

* `filter`

  `ContextFilter`

  A filter to find matching contexts. A context matches if it matches all specified fields in the filter. Any unspecified field in the filter matches all contexts.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (contexts: ExtensionContext[]) => void
  ```

  + `contexts`

    `ExtensionContext[]`

    The matching contexts, if any.

#### Returns

* `Promise<ExtensionContext[]>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getManifest()

```
chrome.runtime.getManifest()
```

Returns details about the app or extension from the manifest. The object returned is a serialization of the full manifest file.

#### Returns

* `object`

  The manifest details.

### getPackageDirectoryEntry()

Promise Foreground only

```
chrome.runtime.getPackageDirectoryEntry( callback?: function, )
```

Returns a `DirectoryEntry` for the package directory.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (directoryEntry: DirectoryEntry) => void
  ```

  + `directoryEntry`

    `DirectoryEntry`

#### Returns

* `Promise<DirectoryEntry>`

  Chrome 122+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getPlatformInfo()

Promise

```
chrome.runtime.getPlatformInfo( callback?: function, )
```

Returns information about the current platform.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (platformInfo: PlatformInfo) => void
  ```

  + `platformInfo`

    `PlatformInfo`

#### Returns

* `Promise<PlatformInfo>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getURL()

```
chrome.runtime.getURL( path: string, )
```

Converts a relative path within an app/extension install directory to a fully-qualified URL.

#### Parameters

* `path`

  `string`

  A path to a resource within an app/extension expressed relative to its install directory.

#### Returns

* `string`

  The fully-qualified URL to the resource.

### openOptionsPage()

Promise

```
chrome.runtime.openOptionsPage( callback?: function, )
```

Open your Extension's options page, if possible.

The precise behavior may depend on your manifest's `options_ui` or `options_page` key, or what Chrome happens to support at the time. For example, the page may be opened in a new tab, within `chrome://extensions`, within an App, or it may just focus an open options page. It will never cause the caller page to reload.

If your Extension does not declare an options page, or Chrome failed to create one for some other reason, the callback will set `lastError`.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### reload()

```
chrome.runtime.reload()
```

Reloads the app or extension. This method is not supported in kiosk mode. For kiosk mode, use `chrome.runtime.restart()` method.

### requestUpdateCheck()

Promise

```
chrome.runtime.requestUpdateCheck( callback?: function, )
```

Requests an immediate update check be done for this app/extension.

Important: Most extensions/apps should not use this method, since Chrome already does automatic checks every few hours, and you can listen for the `runtime.onUpdateAvailable` event without needing to call `requestUpdateCheck`.

This method is only appropriate to call in very limited circumstances, such as if your extension talks to a backend service, and the backend service has determined that the client extension version is very far out of date and you'd like to prompt a user to update. Most other uses of `requestUpdateCheck`, such as calling it unconditionally based on a repeating timer, probably only serve to waste client, network, and server resources.

Note: When called with a callback, instead of returning an object this function will return the two properties as separate arguments passed to the callback.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (result: object) => void
  ```

  + `result`

    `object`

    Chrome 109+

    `RequestUpdateCheckResult` object that holds the status of the update check and any details of the result if there is an update available

    - `status`

      `RequestUpdateCheckStatus`

      Result of the update check.
    - `version`

      `string` optional

      If an update is available, this contains the version of the available update.

#### Returns

* `Promise<object>`

  Chrome 109+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### restart()

```
chrome.runtime.restart()
```

Restart the ChromeOS device when the app runs in kiosk mode. Otherwise, it's no-op.

### restartAfterDelay()

Promise Chrome 53+

```
chrome.runtime.restartAfterDelay( seconds: number, callback?: function, )
```

Restart the ChromeOS device when the app runs in kiosk mode after the given seconds. If called again before the time ends, the reboot will be delayed. If called with a value of -1, the reboot will be cancelled. It's a no-op in non-kiosk mode. It's only allowed to be called repeatedly by the first extension to invoke this API.

#### Parameters

* `seconds`

  `number`

  Time to wait in seconds before rebooting the device, or -1 to cancel a scheduled reboot.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### sendMessage()

Promise

```
chrome.runtime.sendMessage( extensionId?: string, message: any, options?: object, callback?: function, )
```

Sends a single message to event listeners within your extension or a different extension/app. Similar to `runtime.connect` but only sends a single message, with an optional response. If sending to your extension, the `runtime.onMessage` event will be fired in every frame of your extension (except for the sender's frame), or `runtime.onMessageExternal`, if a different extension. Note that extensions cannot send messages to content scripts using this method. To send messages to content scripts, use `tabs.sendMessage`.

#### Parameters

* `extensionId`

  `string` optional

  The ID of the extension to send the message to. If omitted, the message will be sent to your own extension/app. Required if sending messages from a web page for web messaging.
* `message`

  `any`

  The message to send. This message should be a JSON-ifiable object.
* `options`

  `object` optional

  + `includeTlsChannelId`

    `boolean` optional

    Whether the TLS channel ID will be passed into `onMessageExternal` for processes that are listening for the connection event.
* `callback`

  `function` optional

  Chrome 99+

  The callback parameter looks like:

  ```
  (response: any) => void
  ```

  + `response`

    `any`

    The JSON response object sent by the handler of the message. If an error occurs while connecting to the extension, the callback will be called with no arguments and `runtime.lastError` will be set to the error message.

#### Returns

* `Promise<any>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### sendNativeMessage()

Promise

```
chrome.runtime.sendNativeMessage( application: string, message: object, callback?: function, )
```

Send a single message to a native application. This method requires the "nativeMessaging" permission.

#### Parameters

* `application`

  `string`

  The name of the native messaging host.
* `message`

  `object`

  The message that will be passed to the native messaging host.
* `callback`

  `function` optional

  Chrome 99+

  The callback parameter looks like:

  ```
  (response: any) => void
  ```

  + `response`

    `any`

    The response message sent by the native messaging host. If an error occurs while connecting to the native messaging host, the callback will be called with no arguments and `runtime.lastError` will be set to the error message.

#### Returns

* `Promise<any>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setUninstallURL()

Promise

```
chrome.runtime.setUninstallURL( url: string, callback?: function, )
```

Sets the URL to be visited upon uninstallation. This may be used to clean up server-side data, do analytics, and implement surveys. Maximum 1023 characters.

#### Parameters

* `url`

  `string`

  URL to be opened after the extension is uninstalled. This URL must have an `http:` or `https:` scheme. Set an empty string to not open a new tab upon uninstallation.
* `callback`

  `function` optional

  Chrome 45+

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onBrowserUpdateAvailable

Deprecated

```
chrome.runtime.onBrowserUpdateAvailable.addListener( callback: function, )
```

Please use `runtime.onRestartRequired`.

Fired when a Chrome update is available, but isn't installed immediately because a browser restart is required.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  () => void
  ```

### onConnect

```
chrome.runtime.onConnect.addListener( callback: function, )
```

Fired when a connection is made from either an extension process or a content script (by `runtime.connect`).

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (port: Port) => void
  ```

  + `port`

    `Port`

### onConnectExternal

```
chrome.runtime.onConnectExternal.addListener( callback: function, )
```

Fired when a connection is made from another extension (by `runtime.connect`), or from an externally connectable web site.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (port: Port) => void
  ```

  + `port`

    `Port`

### onConnectNative

Chrome 76+

```
chrome.runtime.onConnectNative.addListener( callback: function, )
```

Fired when a connection is made from a native application. This event requires the "nativeMessaging" permission. It is only supported on Chrome OS.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (port: Port) => void
  ```

  + `port`

    `Port`

### onInstalled

```
chrome.runtime.onInstalled.addListener( callback: function, )
```

Fired when the extension is first installed, when the extension is updated to a new version, and when Chrome is updated to a new version.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (details: object) => void
  ```

  + `details`

    `object`

    - `id`

      `string` optional

      Indicates the ID of the imported shared module extension which updated. This is present only if 'reason' is 'shared_module_update'.
    - `previousVersion`

      `string` optional

      Indicates the previous version of the extension, which has just been updated. This is present only if 'reason' is 'update'.
    - `reason`

      `OnInstalledReason`

      The reason that this event is being dispatched.

### onMessage

```
chrome.runtime.onMessage.addListener( callback: function, )
```

Fired when a message is sent from either an extension process (by `runtime.sendMessage`) or a content script (by `tabs.sendMessage`).

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (message: any, sender: MessageSender, sendResponse: function) => boolean | undefined
  ```

  + `message`

    `any`
  + `sender`

    `MessageSender`
  + `sendResponse`

    `function`

    The `sendResponse` parameter looks like:

    ```
    () => void
    ```

  + returns

    `boolean | undefined`

### onMessageExternal

```
chrome.runtime.onMessageExternal.addListener( callback: function, )
```

Fired when a message is sent from another extension (by `runtime.sendMessage`). Cannot be used in a content script.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (message: any, sender: MessageSender, sendResponse: function) => boolean | undefined
  ```

  + `message`

    `any`
  + `sender`

    `MessageSender`
  + `sendResponse`

    `function`

    The `sendResponse` parameter looks like:

    ```
    () => void
    ```

  + returns

    `boolean | undefined`

### onRestartRequired

```
chrome.runtime.onRestartRequired.addListener( callback: function, )
```

Fired when an app or the device that it runs on needs to be restarted. The app should close all its windows at its earliest convenient time to let the restart to happen. If the app does nothing, a restart will be enforced after a 24-hour grace period has passed. Currently, this event is only fired for Chrome OS kiosk apps.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (reason: OnRestartRequiredReason) => void
  ```

  + `reason`

    `OnRestartRequiredReason`

### onStartup

```
chrome.runtime.onStartup.addListener( callback: function, )
```

Fired when a profile that has this extension installed first starts up. This event is not fired when an incognito profile is started, even if this extension is operating in 'split' incognito mode.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  () => void
  ```

### onSuspend

```
chrome.runtime.onSuspend.addListener( callback: function, )
```

Sent to the event page just before it is unloaded. This gives the extension opportunity to do some clean up. Note that since the page is unloading, any asynchronous operations started while handling this event are not guaranteed to complete. If more activity for the event page occurs before it gets unloaded the `onSuspendCanceled` event will be sent and the page won't be unloaded.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  () => void
  ```

### onSuspendCanceled

```
chrome.runtime.onSuspendCanceled.addListener( callback: function, )
```

Sent after `onSuspend` to indicate that the app won't be unloaded after all.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  () => void
  ```

### onUpdateAvailable

```
chrome.runtime.onUpdateAvailable.addListener( callback: function, )
```

Fired when an update is available, but isn't installed immediately because the app is currently running. If you do nothing, the update will be installed the next time the background page gets unloaded, if you want it to be installed sooner you can explicitly call `chrome.runtime.reload()`. If your extension is using a persistent background page, the background page of course never gets unloaded, so unless you call `chrome.runtime.reload()` manually in response to this event the update will not get installed until the next time Chrome itself restarts. If no handlers are listening for this event, and your extension has a persistent background page, it behaves as if `chrome.runtime.reload()` is called in response to this event.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (details: object) => void
  ```

  + `details`

    `object`

    - `version`

      `string`

      The version number of the available update.

### onUserScriptConnect

Chrome 115+ MV3+

```
chrome.runtime.onUserScriptConnect.addListener( callback: function, )
```

Fired when a connection is made from a user script from this extension.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (port: Port) => void
  ```

  + `port`

    `Port`

### onUserScriptMessage

Chrome 115+ MV3+

```
chrome.runtime.onUserScriptMessage.addListener( callback: function, )
```

Fired when a message is sent from a user script associated with the same extension.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (message: any, sender: MessageSender, sendResponse: function) => boolean | undefined
  ```

  + `message`

    `any`
  + `sender`

    `MessageSender`
  + `sendResponse`

    `function`

    The `sendResponse` parameter looks like:

    ```
    () => void
    ```

  + returns

    `boolean | undefined`

</rewritten_file> 

===

---
title: chrome.scripting
url: https://developer.chrome.com/docs/extensions/reference/scripting
---

## Description

Use the `chrome.scripting` API to execute script in different contexts.

## Permissions

`scripting`

## Availability

Chrome 88+ MV3+

## Manifest

To use the `chrome.scripting` API, declare the "scripting" permission in the manifest plus the host permissions for the pages to inject scripts into. Use the `"host_permissions"` key or the `"activeTab"` permission, which grants temporary host permissions. The following example uses the activeTab permission.

```
{
  "name": "Scripting Extension",
  "manifest_version": 3,
  "permissions": ["scripting", "activeTab"],
  ...
}
```

## Concepts and usage

You can use the `chrome.scripting` API to inject JavaScript and CSS into websites. This is similar to what you can do with content scripts. But by using the `chrome.scripting` namespace, extensions can make decisions at runtime.

### Injection targets

You can use the `target` parameter to specify a target to inject JavaScript or CSS into.

The only required field is `tabId`. By default, an injection will run in the main frame of the specified tab.

```
function getTabId() { ... }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId()},
    files : [ "script.js" ],
  })
  .then(() => console.log("script injected"));
```

To run in all frames of the specified tab, you can set the `allFrames` boolean to `true`.

```
function getTabId() { ... }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId(), allFrames : true},
    files : [ "script.js" ],
  })
  .then(() => console.log("script injected in all frames"));
```

You can also inject into specific frames of a tab by specifying individual frame IDs. For more information on frame IDs, see the `chrome.webNavigation` API.

```
function getTabId() { ... }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId(), frameIds : [ frameId1, frameId2 ]},
    files : [ "script.js" ],
  })
  .then(() => console.log("script injected on target frames"));
```

Note: You cannot specify both the `"frameIds"` and `"allFrames"` properties.

### Injected code

Extensions can specify the code to be injected either via an external file or a runtime variable.

#### Files

Files are specified as strings that are paths relative to the extension's root directory. The following code will inject the file `script.js` into the main frame of the tab.

```
function getTabId() { ... }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId()},
    files : [ "script.js" ],
  })
  .then(() => console.log("injected script file"));
```

#### Runtime functions

When injecting JavaScript with `scripting.executeScript()`, you can specify a function to be executed instead of a file. This function should be a function variable available to the current extension context.

```
function getTabId() { ... }
function getTitle() { return document.title; }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId()},
    func : getTitle,
  })
  .then(() => console.log("injected a function"));
```

```
function getTabId() { ... }
function getUserColor() { ... }
function changeBackgroundColor() { document.body.style.backgroundColor = getUserColor(); }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId()},
    func : changeBackgroundColor,
  })
  .then(() => console.log("injected a function"));
```

You can work around this by using the `args` property:

```
function getTabId() { ... }
function getUserColor() { ... }
function changeBackgroundColor(backgroundColor) { document.body.style.backgroundColor = backgroundColor; }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId()},
    func : changeBackgroundColor,
    args : [ getUserColor() ],
  })
  .then(() => console.log("injected a function"));
```

#### Runtime strings

If injecting CSS within a page, you can also specify a string to be used in the `css` property. This option is only available for `scripting.insertCSS()`; you can't execute a string using `scripting.executeScript()`.

```
function getTabId() { ... }
const css = "body { background-color: red; }";
chrome.scripting
  .insertCSS({
    target : {tabId : getTabId()},
    css : css,
  })
  .then(() => console.log("CSS injected"));
```

### Handle the results

The results of executing JavaScript are passed to the extension. A single result is included per-frame. The main frame is guaranteed to be the first index in the resulting array; all other frames are in a non-deterministic order.

```
function getTabId() { ... }
function getTitle() { return document.title; }
chrome.scripting
  .executeScript({
    target : {tabId : getTabId(), allFrames : true},
    func : getTitle,
  })
  .then(injectionResults => {
    for (const {frameId, result} of injectionResults) {
      console.log(`Frame ${frameId} result:`, result);
    }
  });
```

`scripting.insertCSS()` does not return any results.

#### Promises

If the resulting value of the script execution is a promise, Chrome will wait for the promise to settle and return the resulting value.

```
function getTabId() { ... }
async function addIframe() {
  const iframe = document.createElement("iframe");
  const loadComplete = new Promise(resolve => iframe.addEventListener("load", resolve));
  iframe.src = "https://example.com";
  document.body.appendChild(iframe);
  await loadComplete;
  return iframe.contentWindow.document.title;
}
chrome.scripting
  .executeScript({
    target : {tabId : getTabId(), allFrames : true},
    func : addIframe,
  })
  .then(injectionResults => {
    for (const frameResult of injectionResults) {
      const {frameId, result} = frameResult;
      console.log(`Frame ${frameId} result:`, result);
    }
  });
```

## Examples

### Unregister all dynamic content scripts

The following snippet contains a function that unregisters all dynamic content scripts the extension has previously registered.

```
async function unregisterAllDynamicContentScripts() {
  try {
    const scripts = await chrome.scripting.getRegisteredContentScripts();
    const scriptIds = scripts.map(script => script.id);
    return chrome.scripting.unregisterContentScripts({ ids: scriptIds });
  } catch (error) {
    const message = [
      "An unexpected error occurred while",
      "unregistering dynamic content scripts.",
    ].join(" ");
    throw new Error(message, {cause : error});
  }
}
```

Key point: Unregistering content scripts will not remove scripts or styles that have already been injected.

To try the `chrome.scripting` API, install the scripting sample from the Chrome extension samples repository.

## Types

### ContentScriptFilter

Chrome 96+

#### Properties

* `ids`

  `string[]` optional

  If specified, `getRegisteredContentScripts` will only return scripts with an id specified in this list.

### CSSInjection

#### Properties

* `css`

  `string` optional

  A string containing the CSS to inject. Exactly one of `files` and `css` must be specified.
* `files`

  `string[]` optional

  The path of the CSS files to inject, relative to the extension's root directory. Exactly one of `files` and `css` must be specified.
* `origin`

  `StyleOrigin` optional

  The style origin for the injection. Defaults to `'AUTHOR'`.
* `target`

  `InjectionTarget`

  Details specifying the target into which to insert the CSS.

### ExecutionWorld

Chrome 95+

The JavaScript world for a script to execute within.

#### Enum

`"ISOLATED"` Specifies the isolated world, which is the execution environment unique to this extension.

`"MAIN"` Specifies the main world of the DOM, which is the execution environment shared with the host page's JavaScript.

### InjectionResult

#### Properties

* `documentId`

  `string`

  Chrome 106+

  The document associated with the injection.
* `frameId`

  `number`

  Chrome 90+

  The frame associated with the injection.
* `result`

  `any` optional

  The result of the script execution.

### InjectionTarget

#### Properties

* `allFrames`

  `boolean` optional

  Whether the script should inject into all frames within the tab. Defaults to `false`. This must not be `true` if `frameIds` is specified.
* `documentIds`

  `string[]` optional

  Chrome 106+

  The IDs of specific `documentIds` to inject into. This must not be set if `frameIds` is set.
* `frameIds`

  `number[]` optional

  The IDs of specific frames to inject into.
* `tabId`

  `number`

  The ID of the tab into which to inject.

### RegisteredContentScript

Chrome 96+

#### Properties

* `allFrames`

  `boolean` optional

  If specified `true`, it will inject into all frames, even if the frame is not the top-most frame in the tab. Each frame is checked independently for URL requirements; it will not inject into child frames if the URL requirements are not met. Defaults to `false`, meaning that only the top frame is matched.
* `css`

  `string[]` optional

  The list of CSS files to be injected into matching pages. These are injected in the order they appear in this array, before any DOM is constructed or displayed for the page.
* `excludeMatches`

  `string[]` optional

  Excludes pages that this content script would otherwise be injected into. See Match Patterns for more details on the syntax of these strings.
* `id`

  `string`

  The id of the content script, specified in the API call. Must not start with a `'_'` as it's reserved as a prefix for generated script IDs.
* `js`

  `string[]` optional

  The list of JavaScript files to be injected into matching pages. These are injected in the order they appear in this array.
* `matchOriginAsFallback`

  `boolean` optional

  Chrome 119+

  Indicates whether the script can be injected into frames where the URL contains an unsupported scheme; specifically: `about:`, `data:`, `blob:`, or `filesystem:`. In these cases, the URL's origin is checked to determine if the script should be injected. If the origin is null (as is the case for `data:` URLs) then the used origin is either the frame that created the current frame or the frame that initiated the navigation to this frame. Note that this may not be the parent frame.
* `matches`

  `string[]` optional

  Specifies which pages this content script will be injected into. See Match Patterns for more details on the syntax of these strings. Must be specified for `registerContentScripts`.
* `persistAcrossSessions`

  `boolean` optional

  Specifies if this content script will persist into future sessions. The default is `true`.
* `runAt`

  `RunAt` optional

  Specifies when JavaScript files are injected into the web page. The preferred and default value is `document_idle`.
* `world`

  `ExecutionWorld` optional

  Chrome 102+

  The JavaScript `"world"` to run the script in. Defaults to `ISOLATED`.

### ScriptInjection

#### Properties

* `args`

  `any[]` optional

  Chrome 92+

  The arguments to pass to the provided function. This is only valid if the `func` parameter is specified. These arguments must be JSON-serializable.
* `files`

  `string[]` optional

  The path of the JS or CSS files to inject, relative to the extension's root directory. Exactly one of `files` or `func` must be specified.
* `injectImmediately`

  `boolean` optional

  Chrome 102+

  Whether the injection should be triggered in the target as soon as possible. Note that this is not a guarantee that injection will occur prior to page load, as the page may have already loaded by the time the script reaches the target.
* `target`

  `InjectionTarget`

  Details specifying the target into which to inject the script.
* `world`

  `ExecutionWorld` optional

  Chrome 95+

  The JavaScript `"world"` to run the script in. Defaults to `ISOLATED`.
* `func`

  `void` optional

  Chrome 92+

  A JavaScript function to inject. This function will be serialized, and then deserialized for injection. This means that any bound parameters and execution context will be lost. Exactly one of `files` or `func` must be specified.

  The `func` function looks like:

  ```
  () => {...}
  ```

### StyleOrigin

The origin for a style change. See style origins for more info.

#### Enum

`"AUTHOR"`

`"USER"`

## Methods

### executeScript()

Promise

```
chrome.scripting.executeScript( injection: ScriptInjection, callback?: function, )
```

Injects a script into a target context. By default, the script will be run at `document_idle`, or immediately if the page has already loaded. If the `injectImmediately` property is set, the script will inject without waiting, even if the page has not finished loading. If the script evaluates to a promise, the browser will wait for the promise to settle and return the resulting value.

#### Parameters

* `injection`

  `ScriptInjection`

  The details of the script which to inject.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (results: InjectionResult[]) => void
  ```

  + `results`

    `InjectionResult[]`

#### Returns

* `Promise<InjectionResult[]>`

  Chrome 90+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getRegisteredContentScripts()

Promise Chrome 96+

```
chrome.scripting.getRegisteredContentScripts( filter?: ContentScriptFilter, callback?: function, )
```

Returns all dynamically registered content scripts for this extension that match the given filter.

#### Parameters

* `filter`

  `ContentScriptFilter` optional

  An object to filter the extension's dynamically registered scripts.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (scripts: RegisteredContentScript[]) => void
  ```

  + `scripts`

    `RegisteredContentScript[]`

#### Returns

* `Promise<RegisteredContentScript[]>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### insertCSS()

Promise

```
chrome.scripting.insertCSS( injection: CSSInjection, callback?: function, )
```

Inserts a CSS stylesheet into a target context. If multiple frames are specified, unsuccessful injections are ignored.

#### Parameters

* `injection`

  `CSSInjection`

  The details of the styles to insert.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 90+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### registerContentScripts()

Promise Chrome 96+

```
chrome.scripting.registerContentScripts( scripts: RegisteredContentScript[], callback?: function, )
```

Registers one or more content scripts for this extension.

#### Parameters

* `scripts`

  `RegisteredContentScript[]`

  Contains a list of scripts to be registered. If there are errors during script parsing/file validation, or if the IDs specified already exist, then no scripts are registered.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeCSS()

Promise Chrome 90+

```
chrome.scripting.removeCSS( injection: CSSInjection, callback?: function, )
```

Removes a CSS stylesheet that was previously inserted by this extension from a target context.

#### Parameters

* `injection`

  `CSSInjection`

  The details of the styles to remove. Note that the `css`, `files`, and `origin` properties must exactly match the stylesheet inserted through `insertCSS`. Attempting to remove a non-existent stylesheet is a no-op.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 90+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### unregisterContentScripts()

Promise Chrome 96+

```
chrome.scripting.unregisterContentScripts( filter?: ContentScriptFilter, callback?: function, )
```

Unregisters content scripts for this extension.

#### Parameters

* `filter`

  `ContentScriptFilter` optional

  If specified, only unregisters dynamic content scripts which match the filter. Otherwise, all of the extension's dynamic content scripts are unregistered.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### updateContentScripts()

Promise Chrome 96+

```
chrome.scripting.updateContentScripts( scripts: RegisteredContentScript[], callback?: function, )
```

Updates one or more content scripts for this extension.

#### Parameters

* `scripts`

  `RegisteredContentScript[]`

  Contains a list of scripts to be updated. A property is only updated for the existing script if it is specified in this object. If there are errors during script parsing/file validation, or if the IDs specified do not correspond to a fully registered script, then no scripts are updated.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.search
url: https://developer.chrome.com/docs/extensions/reference/search
---

## Description

Use the `chrome.search` API to search via the default provider.

## Permissions

`search`

## Availability

Chrome 87+

## Types

### Disposition

#### Enum

`"CURRENT_TAB"` Specifies that the search results display in the calling tab or the tab from the active browser.

`"NEW_TAB"` Specifies that the search results display in a new tab.

`"NEW_WINDOW"` Specifies that the search results display in a new window.

### QueryInfo

#### Properties

* `disposition`

  `Disposition` optional

  Location where search results should be displayed. `CURRENT_TAB` is the default.
* `tabId`

  `number` optional

  Location where search results should be displayed. `tabId` cannot be used with `disposition`.
* `text`

  `string`

  String to query with the default search provider.

## Methods

### query()

Promise

```
chrome.search.query( queryInfo: QueryInfo, callback?: function, )
```

Used to query the default search provider. In case of an error, `runtime.lastError` will be set.

#### Parameters

* `queryInfo`

  `QueryInfo`
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.sessions
url: https://developer.chrome.com/docs/extensions/reference/sessions
---

## Description

Use the `chrome.sessions` API to query and restore tabs and windows from a browsing session.

## Permissions

`sessions`

## Types

### Device

#### Properties

* `deviceName`

  `string`

  The name of the foreign device.
* `sessions`

  `Session[]`

  A list of open window sessions for the foreign device, sorted from most recently to least recently modified session.

### Filter

#### Properties

* `maxResults`

  `number` optional

  The maximum number of entries to be fetched in the requested list. Omit this parameter to fetch the maximum number of entries (`sessions.MAX_SESSION_RESULTS`).

### Session

#### Properties

* `lastModified`

  `number`

  The time when the window or tab was closed or modified, represented in seconds since the epoch.
* `tab`

  `Tab` optional

  The `tabs.Tab`, if this entry describes a tab. Either this or `sessions.Session.window` will be set.
* `window`

  `Window` optional

  The `windows.Window`, if this entry describes a window. Either this or `sessions.Session.tab` will be set.

## Properties

### MAX_SESSION_RESULTS

The maximum number of `sessions.Session` that will be included in a requested list.

#### Value

25

## Methods

### getDevices()

Promise

```
chrome.sessions.getDevices( filter?: Filter, callback?: function, )
```

Retrieves all devices with synced sessions.

#### Parameters

* `filter`

  `Filter` optional
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (devices: Device[]) => void
  ```

  + `devices`

    `Device[]`

    The list of `sessions.Device` objects for each synced session, sorted in order from device with most recently modified session to device with least recently modified session. `tabs.Tab` objects are sorted by recency in the `windows.Window` of the `sessions.Session` objects.

#### Returns

* `Promise<Device[]>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getRecentlyClosed()

Promise

```
chrome.sessions.getRecentlyClosed( filter?: Filter, callback?: function, )
```

Gets the list of recently closed tabs and/or windows.

#### Parameters

* `filter`

  `Filter` optional
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (sessions: Session[]) => void
  ```

  + `sessions`

    `Session[]`

    The list of closed entries in reverse order that they were closed (the most recently closed tab or window will be at index 0). The entries may contain either tabs or windows.

#### Returns

* `Promise<Session[]>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### restore()

Promise

```
chrome.sessions.restore( sessionId?: string, callback?: function, )
```

Reopens a `windows.Window` or `tabs.Tab`, with an optional callback to run when the entry has been restored.

#### Parameters

* `sessionId`

  `string` optional

  The `windows.Window.sessionId`, or `tabs.Tab.sessionId` to restore. If this parameter is not specified, the most recently closed session is restored.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (restoredSession: Session) => void
  ```

  + `restoredSession`

    `Session`

    A `sessions.Session` containing the restored `windows.Window` or `tabs.Tab` object.

#### Returns

* `Promise<Session>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onChanged

```
chrome.sessions.onChanged.addListener( callback: function, )
```

Fired when recently closed tabs and/or windows are changed. This event does not monitor synced sessions changes.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  () => void
  ``` 

===

---
title: chrome.sidePanel
url: https://developer.chrome.com/docs/extensions/reference/sidePanel
---

## Description

Use the `chrome.sidePanel` API to host content in the browser's side panel alongside the main content of a webpage.

## Permissions

`sidePanel`

To use the Side Panel API, add the "sidePanel" permission in the extension manifest file:

`manifest.json`:

```
{
  "name": "My side panel extension",
  ...
  "permissions": [
    "sidePanel"
  ]
}
```

## Availability

Chrome 114+ MV3+

## Concepts and usage

The Side Panel API allows extensions to display their own UI in the side panel, enabling persistent experiences that complement the user's browsing journey.

Chrome browser side panel UI.

Some features include:

* The side panel remains open when navigating between tabs (if set to do so).
* It can be available only on specific websites.
* As an extension page, side panels have access to all Chrome APIs.
* Within Chrome's settings, users can specify which side the panel should be displayed on.

### Use cases

The following sections demonstrate some common use cases for the Side Panel API. See Extension samples for complete extension examples.

#### Display the same side panel on every site

The side panel can be set initially from the `"default_path"` property in the `"side_panel"` key of the manifest to display the same side panel on every site. This should point to a relative path within the extension directory.

`manifest.json`:

```
{
  "name": "My side panel extension",
  ...
  "side_panel": {
    "default_path": "sidepanel.html"
  }
  ...
}
```

`sidepanel.html`:

```
<!DOCTYPE html>
<html>
  <head>
    <title>My Sidepanel</title>
  </head>
  <body>
    <h1>All sites sidepanel extension</h1>
    <p>This side panel is enabled on all sites</p>
  </body>
</html>
```

#### Enable a side panel on a specific site

An extension can use `sidepanel.setOptions()` to enable a side panel on a specific tab. This example uses `chrome.tabs.onUpdated()` to listen for any updates made to the tab. It checks if the URL is `www.google.com` and enables the side panel. Otherwise, it disables it.

`service-worker.js`:

```
const GOOGLE_ORIGIN = 'https://www.google.com';

chrome.tabs.onUpdated.addListener(async (tabId, info, tab) => {
  if (!tab.url) return;
  const url = new URL(tab.url);

  // Enables the side panel on google.com
  if (url.origin === GOOGLE_ORIGIN) {
    await chrome.sidePanel.setOptions({
      tabId,
      path: 'sidepanel.html',
      enabled: true
    });
  } else {
    // Disables the side panel on all other sites
    await chrome.sidePanel.setOptions({
      tabId,
      enabled: false
    });
  }
});
```

When a user temporarily switches to a tab where the side panel is not enabled, the side panel will be hidden. It will automatically show again when the user switches to a tab where it was previously open.

When the user navigates to a site where the side panel is not enabled, the side panel will close, and the extension won't show in the side panel drop-down menu.

For a complete example, see the Tab-specific side panel sample.

#### Open the side panel by clicking the toolbar icon

Developers can allow users to open the side panel when they click the action toolbar icon with `sidePanel.setPanelBehavior()`. First, declare the `"action"` key in the manifest:

`manifest.json`:

```
{
  "name": "My side panel extension",
  ...
  "action": {
    "default_title": "Click to open panel"
  },
  ...
}
```

Now, add this code to the previous example:

`service-worker.js`:

```
const GOOGLE_ORIGIN = 'https://www.google.com';

// Allows users to open the side panel by clicking on the action toolbar icon
chrome.sidePanel
  .setPanelBehavior({ openPanelOnActionClick: true })
  .catch((error) => console.error(error));

...
```

#### Programmatically open the side panel on user interaction

Chrome 116 introduces `sidePanel.open()`. It allows extensions to open the side panel through an extension user gesture, such as clicking on the action icon. Or a user interaction on an extension page or content script, such as clicking a button. For a complete demo, see the Open Side Panel sample extension.

The following code shows how to open a global side panel on the current window when the user clicks on a context menu. When using `sidePanel.open()`, you must choose the context in which it should open. Use `windowId` to open a global side panel. Alternatively, set the `tabId` to open the side panel only on a specific tab.

`service-worker.js`:

```
chrome.runtime.onInstalled.addListener(() => {
  chrome.contextMenus.create({
    id: 'openSidePanel',
    title: chrome..'Open side panel',
    contexts: ['all']
  });
});

chrome.contextMenus.onClicked.addListener((info, tab) => {
  if (info.menuItemId === 'openSidePanel') {
    // This will open the panel in all the pages on the current window.
    chrome.sidePanel.open({ windowId: tab.windowId });
  }
});
```

Key point: Remember to design your side panel as a useful companion tool for users, improving their browsing experience without unnecessary distractions. Check the Quality Guidelines in the Program Policies for more info.

#### Switch to a different panel

Extensions can use `sidepanel.getOptions()` to retrieve the current side panel. The following example sets a welcome side panel on `runtime.onInstalled()`. Then when the user navigates to a different tab, it replaces it with the main side panel.

`service-worker.js`:

```
const welcomePage = 'sidepanels/welcome-sp.html';
const mainPage = 'sidepanels/main-sp.html';

chrome.runtime.onInstalled.addListener(() => {
  chrome.sidePanel.setOptions({ path: welcomePage });
  chrome.sidePanel.setPanelBehavior({ openPanelOnActionClick: true });
});

chrome.tabs.onActivated.addListener(async ({ tabId }) => {
  const { path } = await chrome.sidePanel.getOptions({ tabId });

  if (path === welcomePage) {
    chrome.sidePanel.setOptions({ path: mainPage });
  }
});
```

See the Multiple side panels sample for the full code.

### Side panel user experience

Users will see Chrome's built-in side panels first. Each side panel displays the extension's icon in the side panel menu. If no icons are included, it will show a placeholder icon with the first letter of the extension's name.

#### Open the side panel

To allow users to open the side panel, use an action icon in combination with `sidePanel.setPanelBehavior()`. Alternatively, make a call to `sidePanel.open()` following a user interaction, such as:

* An action click
* A keyboard shortcut
* A context menu
* A user gesture on an extension page or content script.

#### Pin the side panel

Pin icon in side panel UI.

The side panel toolbar displays a pin icon when your side panel is open. Clicking the icon pins your extension's action icon. Clicking the action icon once pinned will perform the default action for your action icon and will only open the side panel if this has been explicitly configured.

## Examples

For more Side Panel API extensions demos, explore any of the following extensions:

* Dictionary side panel.
* Global side panel.
* Multiple side panels.
* Open Side panel.
* Site-specific side panel.

## Types

### GetPanelOptions

#### Properties

* `tabId`

  `number` optional

  If specified, the side panel options for the given tab will be returned. Otherwise, returns the default side panel options (used for any tab that doesn't have specific settings).

### OpenOptions

Chrome 116+

#### Properties

* `tabId`

  `number` optional

  The tab in which to open the side panel. If the corresponding tab has a tab-specific side panel, the panel will only be open for that tab. If there is not a tab-specific panel, the global panel will be open in the specified tab and any other tabs without a currently-open tab- specific panel. This will override any currently-active side panel (global or tab-specific) in the corresponding tab. At least one of this or `windowId` must be provided.
* `windowId`

  `number` optional

  The window in which to open the side panel. This is only applicable if the extension has a global (non-tab-specific) side panel or `tabId` is also specified. This will override any currently-active global side panel the user has open in the given window. At least one of this or `tabId` must be provided.

### PanelBehavior

#### Properties

* `openPanelOnActionClick`

  `boolean` optional

  Whether clicking the extension's icon will toggle showing the extension's entry in the side panel. Defaults to `false`.

### PanelOptions

#### Properties

* `enabled`

  `boolean` optional

  Whether the side panel should be enabled. This is optional. The default value is `true`.
* `path`

  `string` optional

  The path to the side panel HTML file to use. This must be a local resource within the extension package.
* `tabId`

  `number` optional

  If specified, the side panel options will only apply to the tab with this id. If omitted, these options set the default behavior (used for any tab that doesn't have specific settings). Note: if the same path is set for this `tabId` and the default `tabId`, then the panel for this `tabId` will be a different instance than the panel for the default `tabId`.

### SidePanel

#### Properties

* `default_path`

  `string`

  Developer specified path for side panel display.

## Methods

### getOptions()

Promise

```
chrome.sidePanel.getOptions( options: GetPanelOptions, callback?: function, )
```

Returns the active panel configuration.

#### Parameters

* `options`

  `GetPanelOptions`

  Specifies the context to return the configuration for.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (options: PanelOptions) => void
  ```

  + `options`

    `PanelOptions`

#### Returns

* `Promise<PanelOptions>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getPanelBehavior()

Promise

```
chrome.sidePanel.getPanelBehavior( callback?: function, )
```

Returns the extension's current side panel behavior.

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (behavior: PanelBehavior) => void
  ```

  + `behavior`

    `PanelBehavior`

#### Returns

* `Promise<PanelBehavior>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### open()

Promise Chrome 116+

```
chrome.sidePanel.open( options: OpenOptions, callback?: function, )
```

Opens the side panel for the extension. This may only be called in response to a user action.

#### Parameters

* `options`

  `OpenOptions`

  Specifies the context in which to open the side panel.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setOptions()

Promise

```
chrome.sidePanel.setOptions( options: PanelOptions, callback?: function, )
```

Configures the side panel.

#### Parameters

* `options`

  `PanelOptions`

  The configuration options to apply to the panel.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setPanelBehavior()

Promise

```
chrome.sidePanel.setPanelBehavior( behavior: PanelBehavior, callback?: function, )
```

Configures the extension's side panel behavior. This is an upsert operation.

#### Parameters

* `behavior`

  `PanelBehavior`

  The new behavior to be set.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.storage
url: https://developer.chrome.com/docs/extensions/reference/storage
---

## Description

Use the `chrome.storage` API to store, retrieve, and track changes to user data.

## Permissions

`storage`

To use the storage API, declare the "storage" permission in the extension manifest. For example:

```
{
  "name": "My extension",
  ...
  "permissions": [
    "storage"
  ],
  ...
}
```

## Concepts and usage

The Storage API provides an extension-specific way to persist user data and state. It's similar to the web platform's storage APIs (IndexedDB, and Storage), but was designed to meet the storage needs of extensions. The following are a few key features:

* All extension contexts, including the extension service worker and content scripts have access to the Storage API.
* The JSON serializable values are stored as object properties.
* The Storage API is asynchronous with bulk read and write operations.
* Even if the user clears the cache and browsing history, the data persists.
* Stored settings persist even when using split incognito.
* Includes an exclusive read-only managed storage area for enterprise policies.

### Can extensions use web storage APIs?

While extensions can use the Storage interface (accessible from `window.localStorage`) in some contexts (popup and other HTML pages), we don't recommend it for the following reasons:

* Extension service workers can't use the Web Storage API.
* Content scripts share storage with the host page.
* Data saved using the Web Storage API is lost when the user clears their browsing history.

To move data from web storage APIs to extension storage APIs from a service worker:

1. Prepare an offscreen document html page and script file. The script file should contain a conversion routine and an `onMessage` handler.
2. In the extension service worker, check `chrome.storage` for your data.
3. If your data isn't found, call `createDocument()`.
4. After the returned Promise resolves, call `sendMessage()` to start the conversion routine.
5. Inside the offscreen document's `onMessage` handler, call the conversion routine.

There are also some nuances to how web storage APIs work in extensions. Learn more in the Storage and Cookies article.

### Storage areas

The Storage API is divided into the following storage areas:

`storage.local`
: Data is stored locally and cleared when the extension is removed. The storage limit is 10 MB (5 MB in Chrome 113 and earlier), but can be increased by requesting the "unlimitedStorage" permission. We recommend using `storage.local` to store larger amounts of data.

`storage.managed`
: Managed storage is read-only storage for policy installed extensions and managed by system administrators using a developer-defined schema and enterprise policies. Policies are analogous to options but are configured by a system administrator instead of the user, allowing the extension to be preconfigured for all users of an organization. For information on policies, see Documentation for Administrators. To learn more about the managed storage area, see Manifest for storage areas.

`storage.session`
: Holds data in memory while an extension is loaded. The storage is cleared if the extension is disabled, reloaded or updated and when the browser restarts. By default, it's not exposed to content scripts, but this behavior can be changed by setting `chrome.storage.session.setAccessLevel()`. The storage limit is 10 MB (1 MB in Chrome 111 and earlier). The`storage.session` interface is one of several we recommend for service workers.

`storage.sync`
: If syncing is enabled, the data is synced to any Chrome browser that the user is logged into. If disabled, it behaves like `storage.local`. Chrome stores the data locally when the browser is offline and resumes syncing when it's back online. The quota limitation is approximately 100 KB, 8 KB per item. We recommend using `storage.sync` to preserve user settings across synced browsers. If you're working with sensitive user data, instead use `storage.session`.

### Storage and throttling limits

The Storage API has the following usage limitations:

* Storing data often comes with performance costs, and the API includes storage quotas. We recommend being careful about what data you store so that you don't lose the ability to store data.
* Storage can take time to complete. Make sure to structure your code to account for that time.

For details on storage area limitations and what happens when they're exceeded, see the quota information for sync, local, and session.

## Use cases

The following sections demonstrate common use cases for the Storage API.

### Synchronous response to storage updates

To track changes made to storage, add a listener to its `onChanged` event. When anything changes in storage, that event fires. The sample code listens for these changes:

`background.js`:

```
chrome.storage.onChanged.addListener((changes, namespace) => {
  for (let [key, { oldValue, newValue }] of Object.entries(changes)) {
    console.log(
      `Storage key "${key}" in namespace "${namespace}" changed.`,
      `Old value was "${oldValue}", new value is "${newValue}".`
    );
  }
});
```

We can take this idea even further. In this example, we have an options page that allows the user to toggle a "debug mode" (implementation not shown here). The options page immediately saves the new settings to `storage.sync`, and the service worker uses `storage.onChanged` to apply the setting as soon as possible.

`options.html`:

```
<!-- type="module" allows you to use top level await -->
<script defer src="options.js" type="module"></script>

<form id="optionsForm">
  <label for="debug">
    <input type="checkbox" name="debug" id="debug">
    Enable debug mode
  </label>
</form>
```

`options.js`:

```
// In-page cache of the user's options
const options = {};
const optionsForm = document.getElementById("optionsForm");

// Immediately persist options changes
optionsForm.debug.addEventListener("change", (event) => {
  options.debug = event.target.checked;
  chrome.storage.sync.set({ options });
});

// Initialize the form with the user's option settings
const data = await chrome.storage.sync.get("options");
Object.assign(options, data.options);
optionsForm.debug.checked = Boolean(options.debug);
```

`background.js`:

```
function setDebugMode() { /* ... */ }

// Watch for changes to the user's options & apply them
chrome.storage.onChanged.addListener((changes, area) => {
  if (area === 'sync' && changes.options?.newValue) {
    const debugMode = Boolean(changes.options.newValue.debug);
    console.log('enable debug mode?', debugMode);
    setDebugMode(debugMode);
  }
});
```

### Asynchronous preload from storage

Because service workers don't run all the time, Manifest V3 extensions sometimes need to asynchronously load data from storage before they execute their event handlers. To do this, the following snippet uses an async `action.onClicked` event handler that waits for the `storageCache` global to be populated before executing its logic.

`background.js`:

```
// Where we will expose all the data we retrieve from storage.sync.
const storageCache = { count: 0 };
// Asynchronously retrieve data from storage.sync, then cache it.
const initStorageCache = chrome.storage.sync.get().then((items) => {
  // Copy the data retrieved from storage into storageCache.
  Object.assign(storageCache, items);
});

chrome.action.onClicked.addListener(async (tab) => {
  try {
    await initStorageCache;
  } catch (e) {
    // Handle error that occurred during storage initialization.
  }

  // Normal action handler logic.
  storageCache.count++;
  storageCache.lastTabId = tab.id;
  chrome.storage.sync.set(storageCache);
});
```

## DevTools

You can view and edit data stored using the API in DevTools. To learn more, see the View and edit extension storage page in the DevTools documentation.

## Examples

The following samples demonstrate the local, sync, and session storage areas:

### Local

```
chrome.storage.local.set({ key: value }).then(() => {
  console.log("Value is set");
});

chrome.storage.local.get(["key"]).then((result) => {
  console.log("Value is " + result.key);
});
```

### Sync

```
chrome.storage.sync.set({ key: value }).then(() => {
  console.log("Value is set");
});

chrome.storage.sync.get(["key"]).then((result) => {
  console.log("Value is " + result.key);
});
```

### Session

```
chrome.storage.session.set({ key: value }).then(() => {
  console.log("Value was set");
});

chrome.storage.session.get(["key"]).then((result) => {
  console.log("Value is " + result.key);
});
```

To see other demos of the Storage API, explore any of the following samples:

* Global search extension.
* Water alarm extension.

## Types

### AccessLevel

Chrome 102+

The storage area's access level.

#### Enum

`"TRUSTED_CONTEXTS"` Specifies contexts originating from the extension itself.

`"TRUSTED_AND_UNTRUSTED_CONTEXTS"` Specifies contexts originating from outside the extension.

### StorageArea

#### Properties

* `onChanged`

  `Event<functionvoidvoid>`

  Chrome 73+

  Fired when one or more items change.

  The `onChanged.addListener` function looks like:

  ```
  (callback: function) => {...}
  ```

  + `callback`

    `function`

    The callback parameter looks like:

    ```
    (changes: object) => void
    ```

    - `changes`

      `object`
* `clear`

  `void`

  Promise

  Removes all items from storage.

  The `clear` function looks like:

  ```
  (callback?: function) => {...}
  ```

  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    () => void
    ```

  + returns

    `Promise<void>`

    Chrome 95+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `get`

  `void`

  Promise

  Gets one or more items from storage.

  The `get` function looks like:

  ```
  (keys?: string | string[] | object, callback?: function) => {...}
  ```

  + `keys`

    `string | string[] | object` optional

    A single key to get, list of keys to get, or a dictionary specifying default values (see description of the object). An empty list or object will return an empty result object. Pass in `null` to get the entire contents of storage.
  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    (items: object) => void
    ```

    - `items`

      `object`

      Object with items in their key-value mappings.

  + returns

    `Promise<object>`

    Chrome 95+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `getBytesInUse`

  `void`

  Promise

  Gets the amount of space (in bytes) being used by one or more items.

  The `getBytesInUse` function looks like:

  ```
  (keys?: string | string[], callback?: function) => {...}
  ```

  + `keys`

    `string | string[]` optional

    A single key or list of keys to get the total usage for. An empty list will return 0. Pass in `null` to get the total usage of all of storage.
  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    (bytesInUse: number) => void
    ```

    - `bytesInUse`

      `number`

      Amount of space being used in storage, in bytes.

  + returns

    `Promise<number>`

    Chrome 95+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `getKeys`

  `void`

  Promise Chrome 130+

  Gets all keys from storage.

  The `getKeys` function looks like:

  ```
  (callback?: function) => {...}
  ```

  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    (keys: string[]) => void
    ```

    - `keys`

      `string[]`

      Array with keys read from storage.

  + returns

    `Promise<string[]>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `remove`

  `void`

  Promise

  Removes one or more items from storage.

  The `remove` function looks like:

  ```
  (keys: string | string[], callback?: function) => {...}
  ```

  + `keys`

    `string | string[]`

    A single key or a list of keys for items to remove.
  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    () => void
    ```

  + returns

    `Promise<void>`

    Chrome 95+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `set`

  `void`

  Promise

  Sets multiple items.

  The `set` function looks like:

  ```
  (items: object, callback?: function) => {...}
  ```

  + `items`

    `object`

    An object which gives each key/value pair to update storage with. Any other key/value pairs in storage will not be affected.

    Primitive values such as numbers will serialize as expected. Values with a `typeof "object"` and `"function"` will typically serialize to `{}`, with the exception of Array (serializes as expected), Date, and Regex (serialize using their String representation).
  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    () => void
    ```

  + returns

    `Promise<void>`

    Chrome 95+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `setAccessLevel`

  `void`

  Promise Chrome 102+

  Sets the desired access level for the storage area. The default will be only trusted contexts.

  The `setAccessLevel` function looks like:

  ```
  (accessOptions: object, callback?: function) => {...}
  ```

  + `accessOptions`

    `object`

    - `accessLevel`

      `AccessLevel`

      The access level of the storage area.
  + `callback`

    `function` optional

    The callback parameter looks like:

    ```
    () => void
    ```

  + returns

    `Promise<void>`

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### StorageChange

#### Properties

* `newValue`

  `any` optional

  The new value of the item, if there is a new value.
* `oldValue`

  `any` optional

  The old value of the item, if there was an old value.

## Properties

### local

Items in the local storage area are local to each machine.

#### Type

`StorageArea` & `object`

#### Properties

* `QUOTA_BYTES`

  10485760

  The maximum amount (in bytes) of data that can be stored in local storage, as measured by the JSON stringification of every value plus every key's length. This value will be ignored if the extension has the `unlimitedStorage` permission. Updates that would cause this limit to be exceeded fail immediately and set `runtime.lastError` when using a callback, or a rejected Promise if using async/await.

### managed

Items in the managed storage area are set by an enterprise policy configured by the domain administrator, and are read-only for the extension; trying to modify this namespace results in an error. For information on configuring a policy, see Manifest for storage areas.

#### Type

`StorageArea`

### session

Chrome 102+ MV3+

Items in the session storage area are stored in-memory and will not be persisted to disk.

#### Type

`StorageArea` & `object`

#### Properties

* `QUOTA_BYTES`

  10485760

  The maximum amount (in bytes) of data that can be stored in memory, as measured by estimating the dynamically allocated memory usage of every value and key. Updates that would cause this limit to be exceeded fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.

### sync

Items in the sync storage area are synced using Chrome Sync.

#### Type

`StorageArea` & `object`

#### Properties

* `MAX_ITEMS`

  512

  The maximum number of items that can be stored in sync storage. Updates that would cause this limit to be exceeded will fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.
* `MAX_SUSTAINED_WRITE_OPERATIONS_PER_MINUTE`

  1000000

  Deprecated

  The `storage.sync` API no longer has a sustained write operation quota.
* `MAX_WRITE_OPERATIONS_PER_HOUR`

  1800

  The maximum number of `set`, `remove`, or `clear` operations that can be performed each hour. This is 1 every 2 seconds, a lower ceiling than the short term higher writes-per-minute limit.

  Updates that would cause this limit to be exceeded fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.
* `MAX_WRITE_OPERATIONS_PER_MINUTE`

  120

  The maximum number of `set`, `remove`, or `clear` operations that can be performed each minute. This is 2 per second, providing higher throughput than writes-per-hour over a shorter period of time.

  Updates that would cause this limit to be exceeded fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.
* `QUOTA_BYTES`

  102400

  The maximum total amount (in bytes) of data that can be stored in sync storage, as measured by the JSON stringification of every value plus every key's length. Updates that would cause this limit to be exceeded fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.
* `QUOTA_BYTES_PER_ITEM`

  8192

  The maximum size (in bytes) of each individual item in sync storage, as measured by the JSON stringification of its value plus its key length. Updates containing items larger than this limit will fail immediately and set `runtime.lastError` when using a callback, or when a Promise is rejected.

## Events

### onChanged

```
chrome.storage.onChanged.addListener( callback: function, )
```

Fired when one or more items change.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (changes: object, areaName: string) => void
  ```

  + `changes`

    `object`
  + `areaName`

    `string`

</rewritten_file> 

===

---
title: chrome.system.cpu
url: https://developer.chrome.com/docs/extensions/reference/api/system/cpu
---

# chrome.system.cpu

## Description

Use the `system.cpu` API to query CPU metadata.

## Permissions

`system.cpu`

## Types

### CpuInfo

#### Properties

*   `archName`
    string
    The architecture name of the processors.
*   `features`
    string[]
    A set of feature codes indicating some of the processor's capabilities. The currently supported codes are "mmx", "sse", "sse2", "sse3", "ssse3", "sse4_1", "sse4_2", and "avx".
*   `modelName`
    string
    The model name of the processors.
*   `numOfProcessors`
    number
    The number of logical processors.
*   `processors`
    `ProcessorInfo`[]
    Information about each logical processor.
*   `temperatures`
    number[]
    Chrome 60+
    List of CPU temperature readings from each thermal zone of the CPU. Temperatures are in degrees Celsius.
    Currently supported on Chrome OS only.

### CpuTime

#### Properties

*   `idle`
    number
    The cumulative time spent idle by this processor.
*   `kernel`
    number
    The cumulative time used by kernel programs on this processor.
*   `total`
    number
    The total cumulative time for this processor. This value is equal to `user` + `kernel` + `idle`.
*   `user`
    number
    The cumulative time used by userspace programs on this processor.

### ProcessorInfo

#### Properties

*   `usage`
    `CpuTime`
    Cumulative usage info for this logical processor.

## Methods

### getInfo()

Promise

```
chrome.system.cpu.getInfo(
  callback?: function,
)
```

Queries basic CPU information of the system.

#### Parameters

*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (info: CpuInfo) => void
    ```
    *   `info`
        `CpuInfo`

#### Returns

*   Promise&lt;`CpuInfo`&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.system.display
url: https://developer.chrome.com/docs/extensions/reference/api/system/display
---

# chrome.system.display

## Description

Use the `system.display` API to query display metadata.

## Permissions

`system.display`

## Types

### ActiveState

Chrome 117+

An enum to tell if the display is detected and used by the system. The display is considered 'inactive', if it is not detected by the system (maybe disconnected, or considered disconnected due to sleep mode, etc). This state is used to keep existing display when the all displays are disconnected, for example.

#### Enum

"active"

"inactive"

### Bounds

#### Properties

*   `height`
    number
    The height of the display in pixels.
*   `left`
    number
    The x-coordinate of the upper-left corner.
*   `top`
    number
    The y-coordinate of the upper-left corner.
*   `width`
    number
    The width of the display in pixels.

### DisplayLayout

Chrome 53+

#### Properties

*   `id`
    string
    The unique identifier of the display.
*   `offset`
    number
    The offset of the display along the connected edge. 0 indicates that the topmost or leftmost corners are aligned.
*   `parentId`
    string
    The unique identifier of the parent display. Empty if this is the root.
*   `position`
    `LayoutPosition`
    The layout position of this display relative to the parent. This will be ignored for the root.

### DisplayMode

Chrome 52+

#### Properties

*   `deviceScaleFactor`
    number
    The display mode device scale factor.
*   `height`
    number
    The display mode height in device independent (user visible) pixels.
*   `heightInNativePixels`
    number
    The display mode height in native pixels.
*   `isInterlaced`
    boolean optional
    Chrome 74+
    `True` if this mode is interlaced, `false` if not provided.
*   `isNative`
    boolean
    `True` if the mode is the display's native mode.
*   `isSelected`
    boolean
    `True` if the display mode is currently selected.
*   `refreshRate`
    number
    Chrome 67+
    The display mode refresh rate in hertz.
*   `uiScale`
    number optional
    Deprecated since Chrome 70
    Use `displayZoomFactor`
    The display mode UI scale factor.
*   `width`
    number
    The display mode width in device independent (user visible) pixels.
*   `widthInNativePixels`
    number
    The display mode width in native pixels.

### DisplayProperties

#### Properties

*   `boundsOriginX`
    number optional
    If set, updates the display's logical bounds origin along the x-axis. Applied together with `boundsOriginY`. Defaults to the current value if not set and `boundsOriginY` is set. Note that when updating the display origin, some constraints will be applied, so the final bounds origin may be different than the one set. The final bounds can be retrieved using `getInfo`. The bounds origin cannot be changed on the primary display.
*   `boundsOriginY`
    number optional
    If set, updates the display's logical bounds origin along the y-axis. See documentation for `boundsOriginX` parameter.
*   `displayMode`
    `DisplayMode` optional
    Chrome 52+
    If set, updates the display mode to the mode matching this value. If other parameters are invalid, this will not be applied. If the display mode is invalid, it will not be applied and an error will be set, but other properties will still be applied.
*   `displayZoomFactor`
    number optional
    Chrome 65+
    If set, updates the zoom associated with the display. This zoom performs re-layout and repaint thus resulting in a better quality zoom than just performing a pixel by pixel stretch enlargement.
*   `isPrimary`
    boolean optional
    If set to `true`, makes the display primary. No-op if set to `false`. Note: If set, the display is considered primary for all other properties (i.e. `isUnified` may be set and bounds origin may not).
*   `isUnified`
    boolean optional
    Chrome 59+
    ChromeOS only. If set to `true`, changes the display mode to unified desktop (see `enableUnifiedDesktop` for details). If set to `false`, unified desktop mode will be disabled. This is only valid for the primary display. If provided, `mirroringSourceId` must not be provided and other properties will be ignored. This is has no effect if not provided.
*   `mirroringSourceId`
    string optional
    Deprecated since Chrome 68
    Use `setMirrorMode`.
    ChromeOS only. If set and not empty, enables mirroring for this display only. Otherwise disables mirroring for all displays. This value should indicate the id of the source display to mirror, which must not be the same as the id passed to `setDisplayProperties`. If set, no other property may be set.
*   `overscan`
    `Insets` optional
    If set, sets the display's overscan insets to the provided values. Note that overscan values may not be negative or larger than a half of the screen's size. Overscan cannot be changed on the internal monitor.
*   `rotation`
    number optional
    If set, updates the display's rotation. Legal values are [0, 90, 180, 270]. The rotation is set clockwise, relative to the display's vertical position.

### DisplayUnitInfo

#### Properties

*   `activeState`
    `ActiveState`
    Chrome 117+
    Active if the display is detected and used by the system.
*   `availableDisplayZoomFactors`
    number[]
    Chrome 67+
    A list of zoom factor values that can be set for the display.
*   `bounds`
    `Bounds`
    The display's logical bounds.
*   `displayZoomFactor`
    number
    Chrome 65+
    The ratio between the display's current and default zoom. For example, value 1 is equivalent to 100% zoom, and value 1.5 is equivalent to 150% zoom.
*   `dpiX`
    number
    The number of pixels per inch along the x-axis.
*   `dpiY`
    number
    The number of pixels per inch along the y-axis.
*   `edid`
    `Edid` optional
    Chrome 67+
    NOTE: This is only available to ChromeOS Kiosk apps and Web UI.
*   `hasTouchSupport`
    boolean
    Chrome 57+
    `True` if this display has a touch input device associated with it.
*   `id`
    string
    The unique identifier of the display.
*   `isEnabled`
    boolean
    `True` if this display is enabled.
*   `isPrimary`
    boolean
    `True` if this is the primary display.
*   `isUnified`
    boolean
    Chrome 59+
    `True` for all displays when in unified desktop mode. See documentation for `enableUnifiedDesktop`.
*   `mirroringDestinationIds`
    string[]
    Chrome 64+
    ChromeOS only. Identifiers of the displays to which the source display is being mirrored. Empty if no displays are being mirrored. This will be set to the same value for all displays. This must not include `mirroringSourceId`.
*   `mirroringSourceId`
    string
    ChromeOS only. Identifier of the display that is being mirrored if mirroring is enabled, otherwise empty. This will be set for all displays (including the display being mirrored).
*   `modes`
    `DisplayMode`[]
    Chrome 52+
    The list of available display modes. The current mode will have `isSelected=true`. Only available on ChromeOS. Will be set to an empty array on other platforms.
*   `name`
    string
    The user-friendly name (e.g. "HP LCD monitor").
*   `overscan`
    `Insets`
    The display's insets within its screen's bounds. Currently exposed only on ChromeOS. Will be set to empty insets on other platforms.
*   `rotation`
    number
    The display's clockwise rotation in degrees relative to the vertical position. Currently exposed only on ChromeOS. Will be set to 0 on other platforms. A value of -1 will be interpreted as auto-rotate when the device is in a physical tablet state.
*   `workArea`
    `Bounds`
    The usable work area of the display within the display bounds. The work area excludes areas of the display reserved for OS, for example taskbar and launcher.

### Edid

Chrome 67+

#### Properties

*   `manufacturerId`
    string
    3 character manufacturer code. See Sec. 3.4.1 page 21. Required in v1.4.
*   `productId`
    string
    2 byte manufacturer-assigned code, Sec. 3.4.2 page 21. Required in v1.4.
*   `yearOfManufacture`
    number
    Year of manufacturer, Sec. 3.4.4 page 22. Required in v1.4.

### GetInfoFlags

Chrome 59+

#### Properties

*   `singleUnified`
    boolean optional
    If set to `true`, only a single `DisplayUnitInfo` will be returned by `getInfo` when in unified desktop mode (see `enableUnifiedDesktop`). Defaults to `false`.

### Insets

#### Properties

*   `bottom`
    number
    The y-axis distance from the bottom bound.
*   `left`
    number
    The x-axis distance from the left bound.
*   `right`
    number
    The x-axis distance from the right bound.
*   `top`
    number
    The y-axis distance from the top bound.

### LayoutPosition

Chrome 53+

Layout position, i.e. edge of parent that the display is attached to.

#### Enum

"top"

"right"

"bottom"

"left"

### MirrorMode

Chrome 65+

Mirror mode, i.e. different ways of how a display is mirrored to other displays.

#### Enum

"off" Specifies the default mode (extended or unified desktop).

"normal" Specifies that the default source display will be mirrored to all other displays.

"mixed" Specifies that the specified source display will be mirrored to the provided destination displays. All other connected displays will be extended.

### MirrorModeInfo

Chrome 65+

#### Properties

*   `mirroringDestinationIds`
    string[] optional
    The ids of the mirroring destination displays. This is only valid for 'mixed'.
*   `mirroringSourceId`
    string optional
    The id of the mirroring source display. This is only valid for 'mixed'.
*   `mode`
    `MirrorMode`
    The mirror mode that should be set.

### Point

Chrome 57+

#### Properties

*   `x`
    number
    The x-coordinate of the point.
*   `y`
    number
    The y-coordinate of the point.

### TouchCalibrationPair

Chrome 57+

#### Properties

*   `displayPoint`
    `Point`
    The coordinates of the display point.
*   `touchPoint`
    `Point`
    The coordinates of the touch point corresponding to the display point.

### TouchCalibrationPairQuad

Chrome 57+

#### Properties

*   `pair1`
    `TouchCalibrationPair`
    First pair of touch and display point required for touch calibration.
*   `pair2`
    `TouchCalibrationPair`
    Second pair of touch and display point required for touch calibration.
*   `pair3`
    `TouchCalibrationPair`
    Third pair of touch and display point required for touch calibration.
*   `pair4`
    `TouchCalibrationPair`
    Fourth pair of touch and display point required for touch calibration.

## Methods

### clearTouchCalibration()

Chrome 57+

```
chrome.system.display.clearTouchCalibration(id: string)
```

Resets the touch calibration for the display and brings it back to its default state by clearing any touch calibration data associated with the display.

#### Parameters

*   `id`
    string
    The display's unique identifier.

### completeCustomTouchCalibration()

Chrome 57+

```
chrome.system.display.completeCustomTouchCalibration(
  pairs: TouchCalibrationPairQuad,
  bounds: Bounds,
)
```

Sets the touch calibration pairs for a display. These pairs would be used to calibrate the touch screen for display with id called in `startCustomTouchCalibration()`. Always call `startCustomTouchCalibration` before calling this method. If another touch calibration is already in progress this will throw an error.

#### Parameters

*   `pairs`
    `TouchCalibrationPairQuad`
    The pairs of point used to calibrate the display.
*   `bounds`
    `Bounds`
    Bounds of the display when the touch calibration was performed. `bounds.left` and `bounds.top` values are ignored.

### enableUnifiedDesktop()

Chrome 46+

```
chrome.system.display.enableUnifiedDesktop(enabled: boolean)
```

Enables/disables the unified desktop feature. If enabled while mirroring is active, the desktop mode will not change until mirroring is turned off. Otherwise, the desktop mode will switch to unified immediately. NOTE: This is only available to ChromeOS Kiosk apps and Web UI.

#### Parameters

*   `enabled`
    boolean
    `True` if unified desktop should be enabled.

### getDisplayLayout()

Promise Chrome 53+

```
chrome.system.display.getDisplayLayout(callback?: function)
```

Requests the layout info for all displays. NOTE: This is only available to ChromeOS Kiosk apps and Web UI.

#### Parameters

*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (layouts: DisplayLayout[]) => void
    ```
    *   `layouts`
        `DisplayLayout`[]

#### Returns

*   Promise&lt;`DisplayLayout`[]&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getInfo()

Promise

```
chrome.system.display.getInfo(
  flags?: GetInfoFlags,
  callback?: function,
)
```

Requests the information for all attached display devices.

#### Parameters

*   `flags`
    `GetInfoFlags` optional
    Chrome 59+
    Options affecting how the information is returned.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (displayInfo: DisplayUnitInfo[]) => void
    ```
    *   `displayInfo`
        `DisplayUnitInfo`[]

#### Returns

*   Promise&lt;`DisplayUnitInfo`[]&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### overscanCalibrationAdjust()

Chrome 53+

```
chrome.system.display.overscanCalibrationAdjust(
  id: string,
  delta: Insets,
)
```

Adjusts the current overscan insets for a display. Typically this should either move the display along an axis (e.g. left+right have the same value) or scale it along an axis (e.g. top+bottom have opposite values). Each Adjust call is cumulative with previous calls since Start.

#### Parameters

*   `id`
    string
    The display's unique identifier.
*   `delta`
    `Insets`
    The amount to change the overscan insets.

### overscanCalibrationComplete()

Chrome 53+

```
chrome.system.display.overscanCalibrationComplete(id: string)
```

Complete overscan adjustments for a display by saving the current values and hiding the overlay.

#### Parameters

*   `id`
    string
    The display's unique identifier.

### overscanCalibrationReset()

Chrome 53+

```
chrome.system.display.overscanCalibrationReset(id: string)
```

Resets the overscan insets for a display to the last saved value (i.e before Start was called).

#### Parameters

*   `id`
    string
    The display's unique identifier.

### overscanCalibrationStart()

Chrome 53+

```
chrome.system.display.overscanCalibrationStart(id: string)
```

Starts overscan calibration for a display. This will show an overlay on the screen indicating the current overscan insets. If overscan calibration for display `id` is in progress this will reset calibration.

#### Parameters

*   `id`
    string
    The display's unique identifier.

### setDisplayLayout()

Promise Chrome 53+

```
chrome.system.display.setDisplayLayout(
  layouts: DisplayLayout[],
  callback?: function,
)
```

Set the layout for all displays. Any display not included will use the default layout. If a layout would overlap or be otherwise invalid it will be adjusted to a valid layout. After layout is resolved, an `onDisplayChanged` event will be triggered. NOTE: This is only available to ChromeOS Kiosk apps and Web UI.

#### Parameters

*   `layouts`
    `DisplayLayout`[]
    The layout information, required for all displays except the primary display.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setDisplayProperties()

Promise

```
chrome.system.display.setDisplayProperties(
  id: string,
  info: DisplayProperties,
  callback?: function,
)
```

Updates the properties for the display specified by `id`, according to the information provided in `info`. On failure, `runtime.lastError` will be set. NOTE: This is only available to ChromeOS Kiosk apps and Web UI.

#### Parameters

*   `id`
    string
    The display's unique identifier.
*   `info`
    `DisplayProperties`
    The information about display properties that should be changed. A property will be changed only if a new value for it is specified in info.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setMirrorMode()

Promise Chrome 65+

```
chrome.system.display.setMirrorMode(
  info: MirrorModeInfo,
  callback?: function,
)
```

Sets the display mode to the specified mirror mode. Each call resets the state from previous calls. Calling `setDisplayProperties()` will fail for the mirroring destination displays. NOTE: This is only available to ChromeOS Kiosk apps and Web UI.

#### Parameters

*   `info`
    `MirrorModeInfo`
    The information of the mirror mode that should be applied to the display mode.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### showNativeTouchCalibration()

Promise Chrome 57+

```
chrome.system.display.showNativeTouchCalibration(
  id: string,
  callback?: function,
)
```

Displays the native touch calibration UX for the display with `id` as display id. This will show an overlay on the screen with required instructions on how to proceed. The callback will be invoked in case of successful calibration only. If the calibration fails, this will throw an error.

#### Parameters

*   `id`
    string
    The display's unique identifier.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (success: boolean) => void
    ```
    *   `success`
        boolean

#### Returns

*   Promise&lt;boolean&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### startCustomTouchCalibration()

Chrome 57+

```
chrome.system.display.startCustomTouchCalibration(id: string)
```

Starts custom touch calibration for a display. This should be called when using a custom UX for collecting calibration data. If another touch calibration is already in progress this will throw an error.

#### Parameters

*   `id`
    string
    The display's unique identifier.

## Events

### onDisplayChanged

```
chrome.system.display.onDisplayChanged.addListener(callback: function)
```

Fired when anything changes to the display configuration.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    () => void
    ``` 

===

---
title: chrome.system.memory
url: https://developer.chrome.com/docs/extensions/reference/api/system/memory
---

# chrome.system.memory

## Description

The `chrome.system.memory` API.

## Permissions

`system.memory`

## Types

### MemoryInfo

#### Properties

*   `availableCapacity`
    number
    The amount of available capacity, in bytes.
*   `capacity`
    number
    The total amount of physical memory capacity, in bytes.

## Methods

### getInfo()

Promise

```
chrome.system.memory.getInfo(
  callback?: function,
)
```

Get physical memory information.

#### Parameters

*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (info: MemoryInfo) => void
    ```
    *   `info`
        `MemoryInfo`

#### Returns

*   Promise&lt;`MemoryInfo`&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.system.storage
url: https://developer.chrome.com/docs/extensions/reference/api/system/storage
---

# chrome.system.storage

## Description

Use the `chrome.system.storage` API to query storage device information and be notified when a removable storage device is attached and detached.

## Permissions

`system.storage`

## Types

### EjectDeviceResultCode

#### Enum

"success" The ejection command is successful -- the application can prompt the user to remove the device.

"in_use" The device is in use by another application. The ejection did not succeed; the user should not remove the device until the other application is done with the device.

"no_such_device" There is no such device known.

"failure" The ejection command failed.

### StorageAvailableCapacityInfo

#### Properties

*   `availableCapacity`
    number
    The available capacity of the storage device, in bytes.
*   `id`
    string
    A copied id of `getAvailableCapacity` function parameter id.

### StorageUnitInfo

#### Properties

*   `capacity`
    number
    The total amount of the storage space, in bytes.
*   `id`
    string
    The transient ID that uniquely identifies the storage device. This ID will be persistent within the same run of a single application. It will not be a persistent identifier between different runs of an application, or between different applications.
*   `name`
    string
    The name of the storage unit.
*   `type`
    `StorageUnitType`
    The media type of the storage unit.

### StorageUnitType

#### Enum

"fixed" The storage has fixed media, e.g. hard disk or SSD.

"removable" The storage is removable, e.g. USB flash drive.

"unknown" The storage type is unknown.

## Methods

### ejectDevice()

Promise

```
chrome.system.storage.ejectDevice(
  id: string,
  callback?: function,
)
```

Ejects a removable storage device.

#### Parameters

*   `id`
    string
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (result: EjectDeviceResultCode) => void
    ```
    *   `result`
        `EjectDeviceResultCode`

#### Returns

*   Promise&lt;`EjectDeviceResultCode`&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAvailableCapacity()

Promise Dev channel

```
chrome.system.storage.getAvailableCapacity(
  id: string,
  callback?: function,
)
```

Get the available capacity of a specified id storage device. The `id` is the transient device ID from `StorageUnitInfo`.

#### Parameters

*   `id`
    string
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (info: StorageAvailableCapacityInfo) => void
    ```
    *   `info`
        `StorageAvailableCapacityInfo`

#### Returns

*   Promise&lt;`StorageAvailableCapacityInfo`&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getInfo()

Promise

```
chrome.system.storage.getInfo(callback?: function)
```

Get the storage information from the system. The argument passed to the callback is an array of `StorageUnitInfo` objects.

#### Parameters

*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (info: StorageUnitInfo[]) => void
    ```
    *   `info`
        `StorageUnitInfo`[]

#### Returns

*   Promise&lt;`StorageUnitInfo`[]&gt;
    Chrome 91+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onAttached

```
chrome.system.storage.onAttached.addListener(callback: function)
```

Fired when a new removable storage is attached to the system.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (info: StorageUnitInfo) => void
    ```
    *   `info`
        `StorageUnitInfo`

### onDetached

```
chrome.system.storage.onDetached.addListener(callback: function)
```

Fired when a removable storage is detached from the system.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (id: string) => void
    ```
    *   `id`
        string

</rewritten_file> 

===

---
title: chrome.systemLog
url: https://developer.chrome.com/docs/extensions/reference/api/systemLog
---

# chrome.systemLog

Important: This API works only on ChromeOS.

## Description

Use the `chrome.systemLog` API to record Chrome system logs from extensions.

## Permissions

`systemLog`

## Availability

Chrome 125+ ChromeOS only Requires policy

## Types

### MessageOptions

#### Properties

*   `message`
    string

## Methods

### add()

Promise

```
chrome.systemLog.add(
  options: MessageOptions,
  callback?: function,
)
```

Adds a new log record.

#### Parameters

*   `options`
    `MessageOptions`
    The logging options.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.tabCapture
url: https://developer.chrome.com/docs/extensions/reference/tabCapture
---

## Description

Use the `chrome.tabCapture` API to interact with tab media streams.

## Permissions

`tabCapture`

## Concepts and usage

The `chrome.tabCapture` API lets you access a `MediaStream` containing video and audio of the current tab. It can only be called after the user invokes an extension, such as by clicking the extension's action button. This is similar to the behavior of the "activeTab" permission.

### Preserve system audio

When a `MediaStream` is obtained for a tab, audio in that tab will no longer be played to the user. This is similar to the behavior of the `getDisplayMedia()` function when the `suppressLocalAudioPlayback` flag is set to true.

To continue playing audio to the user, use the following:

```
const output = new AudioContext();
const source = output.createMediaStreamSource(stream);
source.connect(output.destination);
```

This creates a new `AudioContext` and connects the audio of the tab's `MediaStream` to the default destination.

### Stream IDs

Calling `chrome.tabCapture.getMediaStreamId()` will return a stream ID. To later access a `MediaStream` from the ID, use the following:

```
navigator.mediaDevices.getUserMedia({
  audio: {
    mandatory: {
      chromeMediaSource: "tab",
      chromeMediaSourceId: id,
    },
  },
  video: {
    mandatory: {
      chromeMediaSource: "tab",
      chromeMediaSourceId: id,
    },
  },
});
```

### Usage restrictions

After calling `getMediaStreamId()`, there are restrictions on where the returned stream ID can be used:

* If `consumerTabId` is specified, the ID can be used by a `getUserMedia()` call in any frame in the given tab which has the same security origin.
* When this is not specified, beginning in Chrome 116, the ID can be used in any frame with the same security origin in the same render process as the caller. This means that a stream ID obtained in a service worker can be used in an offscreen document.

Prior to Chrome 116, when a `consumerTabId` was not specified, the stream ID was restricted to both the security origin, render process and render frame of the caller.

### Learn more

To learn more about how to use the `chrome.tabCapture` API, see Audio recording and screen capture. This demonstrates how to use `tabCapture` and related APIs to solve a number of common use cases.

## Types

### CaptureInfo

#### Properties

* `fullscreen`

  `boolean`

  Whether an element in the tab being captured is in fullscreen mode.
* `status`

  `TabCaptureState`

  The new capture status of the tab.
* `tabId`

  `number`

  The id of the tab whose status changed.

### CaptureOptions

#### Properties

* `audio`

  `boolean` optional
* `audioConstraints`

  `MediaStreamConstraint` optional
* `video`

  `boolean` optional
* `videoConstraints`

  `MediaStreamConstraint` optional

### GetMediaStreamOptions

Chrome 71+

#### Properties

* `consumerTabId`

  `number` optional

  Optional tab id of the tab which will later invoke `getUserMedia()` to consume the stream. If not specified then the resulting stream can be used only by the calling extension. The stream can only be used by frames in the given tab whose security origin matches the consumber tab's origin. The tab's origin must be a secure origin, e.g. HTTPS.
* `targetTabId`

  `number` optional

  Optional tab id of the tab which will be captured. If not specified then the current active tab will be selected. Only tabs for which the extension has been granted the activeTab permission can be used as the target tab.

### MediaStreamConstraint

#### Properties

* `mandatory`

  `object`
* `optional`

  `object` optional

### TabCaptureState

#### Enum

`"pending"`

`"active"`

`"stopped"`

`"error"`

## Methods

### capture()

Foreground only

```
chrome.tabCapture.capture( options: CaptureOptions, callback: function, )
```

Captures the visible area of the currently active tab. Capture can only be started on the currently active tab after the extension has been invoked, similar to the way that activeTab works. Capture is maintained across page navigations within the tab, and stops when the tab is closed, or the media stream is closed by the extension.

#### Parameters

* `options`

  `CaptureOptions`

  Configures the returned media stream.
* `callback`

  `function`

  The callback parameter looks like:

  ```
  (stream: LocalMediaStream) => void
  ```

  + `stream`

    `LocalMediaStream`

### getCapturedTabs()

Promise

```
chrome.tabCapture.getCapturedTabs( callback?: function, )
```

Returns a list of tabs that have requested capture or are being captured, i.e. status != stopped and status != error. This allows extensions to inform the user that there is an existing tab capture that would prevent a new tab capture from succeeding (or to prevent redundant requests for the same tab).

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (result: CaptureInfo[]) => void
  ```

  + `result`

    `CaptureInfo[]`

#### Returns

* `Promise<CaptureInfo[]>`

  Chrome 116+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getMediaStreamId()

Promise Chrome 71+

```
chrome.tabCapture.getMediaStreamId( options?: GetMediaStreamOptions, callback?: function, )
```

Creates a stream ID to capture the target tab. Similar to `chrome.tabCapture.capture()` method, but returns a media stream ID, instead of a media stream, to the consumer tab.

#### Parameters

* `options`

  `GetMediaStreamOptions` optional
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (streamId: string) => void
  ```

  + `streamId`

    `string`

#### Returns

* `Promise<string>`

  Chrome 116+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onStatusChanged

```
chrome.tabCapture.onStatusChanged.addListener( callback: function, )
```

Event fired when the capture status of a tab changes. This allows extension authors to keep track of the capture status of tabs to keep UI elements like page actions in sync.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (info: CaptureInfo) => void
  ```

  + `info`

    `CaptureInfo` 

===

---
title: chrome.tabGroups
url: https://developer.chrome.com/docs/extensions/reference/api/tabGroups
---

# chrome.tabGroups

## Description

Use the `chrome.tabGroups` API to interact with the browser's tab grouping system. You can use this API to modify and rearrange tab groups in the browser. To group and ungroup tabs, or to query what tabs are in groups, use the `chrome.tabs` API.

## Permissions

`tabGroups`

## Availability

Chrome 89+ MV3+

## Types

### Color

The group's color.

#### Enum

"grey"

"blue"

"red"

"yellow"

"green"

"pink"

"purple"

"cyan"

"orange"

### TabGroup

#### Properties

*   `collapsed`
    boolean
    Whether the group is collapsed. A collapsed group is one whose tabs are hidden.
*   `color`
    `Color`
    The group's color.
*   `id`
    number
    The ID of the group. Group IDs are unique within a browser session.
*   `shared`
    boolean
    Pending
    Whether the group is shared.
*   `title`
    string optional
    The title of the group.
*   `windowId`
    number
    The ID of the window that contains the group.

## Properties

### TAB_GROUP_ID_NONE

An ID that represents the absence of a group.

#### Value

-1

## Methods

### get()

Promise

```
chrome.tabGroups.get(
  groupId: number,
  callback?: function,
)
```

Retrieves details about the specified group.

#### Parameters

*   `groupId`
    number
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (group: TabGroup) => void
    ```
    *   `group`
        `TabGroup`

#### Returns

*   Promise&lt;`TabGroup`&gt;
    Chrome 90+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### move()

Promise

```
chrome.tabGroups.move(
  groupId: number,
  moveProperties: object,
  callback?: function,
)
```

Moves the group and all its tabs within its window, or to a new window.

#### Parameters

*   `groupId`
    number
    The ID of the group to move.
*   `moveProperties`
    object
    *   `index`
        number
        The position to move the group to. Use -1 to place the group at the end of the window.
    *   `windowId`
        number optional
        The window to move the group to. Defaults to the window the group is currently in. Note that groups can only be moved to and from windows with `windows.WindowType` type "normal".
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (group?: TabGroup) => void
    ```
    *   `group`
        `TabGroup` optional
        Details about the moved group.

#### Returns

*   Promise&lt;`TabGroup` | undefined&gt;
    Chrome 90+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### query()

Promise

```
chrome.tabGroups.query(
  queryInfo: object,
  callback?: function,
)
```

Gets all groups that have the specified properties, or all groups if no properties are specified.

#### Parameters

*   `queryInfo`
    object
    *   `collapsed`
        boolean optional
        Whether the groups are collapsed.
    *   `color`
        `Color` optional
        The color of the groups.
    *   `shared`
        boolean optional
        Pending
        Whether the group is shared.
    *   `title`
        string optional
        Match group titles against a pattern.
    *   `windowId`
        number optional
        The ID of the parent window, or `windows.WINDOW_ID_CURRENT` for the current window.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (result: TabGroup[]) => void
    ```
    *   `result`
        `TabGroup`[]

#### Returns

*   Promise&lt;`TabGroup`[]&gt;
    Chrome 90+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### update()

Promise

```
chrome.tabGroups.update(
  groupId: number,
  updateProperties: object,
  callback?: function,
)
```

Modifies the properties of a group. Properties that are not specified in `updateProperties` are not modified.

#### Parameters

*   `groupId`
    number
    The ID of the group to modify.
*   `updateProperties`
    object
    *   `collapsed`
        boolean optional
        Whether the group should be collapsed.
    *   `color`
        `Color` optional
        The color of the group.
    *   `title`
        string optional
        The title of the group.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (group?: TabGroup) => void
    ```
    *   `group`
        `TabGroup` optional
        Details about the updated group.

#### Returns

*   Promise&lt;`TabGroup` | undefined&gt;
    Chrome 90+
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onCreated

```
chrome.tabGroups.onCreated.addListener(callback: function)
```

Fired when a group is created.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (group: TabGroup) => void
    ```
    *   `group`
        `TabGroup`

### onMoved

```
chrome.tabGroups.onMoved.addListener(callback: function)
```

Fired when a group is moved within a window. Move events are still fired for the individual tabs within the group, as well as for the group itself. This event is not fired when a group is moved between windows; instead, it will be removed from one window and created in another.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (group: TabGroup) => void
    ```
    *   `group`
        `TabGroup`

### onRemoved

```
chrome.tabGroups.onRemoved.addListener(callback: function)
```

Fired when a group is closed, either directly by the user or automatically because it contained zero tabs.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (group: TabGroup) => void
    ```
    *   `group`
        `TabGroup`

### onUpdated

```
chrome.tabGroups.onUpdated.addListener(callback: function)
```

Fired when a group is updated.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (group: TabGroup) => void
    ```
    *   `group`
        `TabGroup`

</rewritten_file> 

===

---
title: chrome.tabs
url: https://developer.chrome.com/docs/extensions/reference/tabs
---

Note: The Tabs API can be used by the service worker and extension pages, but not content scripts.

## Description

Use the `chrome.tabs` API to interact with the browser's tab system. You can use this API to create, modify, and rearrange tabs in the browser.

The Tabs API not only offers features for manipulating and managing tabs, but can also detect the language of the tab, take a screenshot, and communicate with a tab's content scripts.

## Permissions

Most features don't require any permissions to use. For example: creating a new tab, reloading a tab, navigating to another URL, etc.

There are three permissions developers should be aware of when working with the Tabs API.

The "tabs" permission
: This permission does not give access to the `chrome.tabs` namespace. Instead, it grants an extension the ability to call `tabs.query()` against four sensitive properties on `tabs.Tab` instances: `url`, `pendingUrl`, `title`, and `favIconUrl`.

  ```
  {
    "name": "My extension",
    ...
    "permissions": [
      "tabs"
    ],
    ...
  }
  ```

Host permissions
: Host permissions allow an extension to read and query a matching tab's four sensitive `tabs.Tab` properties. They can also interact directly with the matching tabs using methods such as `tabs.captureVisibleTab()`, `scripting.executeScript()`, `scripting.insertCSS()`, and `scripting.removeCSS()`.

  ```
  {
    "name": "My extension",
    ...
    "host_permissions": [
      "http://*/*",
      "https://*/*"
    ],
    ...
  }
  ```

The "activeTab" permission
: `activeTab` grants an extension temporary host permission for the current tab in response to a user invocation. Unlike host permissions, `activeTab` does not trigger any warnings.

  ```
  {
    "name": "My extension",
    ...
    "permissions": [
      "activeTab"
    ],
    ...
  }
  ```

## Use cases

The following sections demonstrate some common use cases.

### Open an extension page in a new tab

A common pattern for extensions is to open an onboarding page in a new tab when the extension is installed. The following example shows how to do this.

`background.js`:

```
chrome.runtime.onInstalled.addListener(({reason}) => {
  if (reason === 'install') {
    chrome.tabs.create({ url: "onboarding.html" });
  }
});
```

Note: This example doesn't require any permissions.

### Get the current tab

This example demonstrates how an extension's service worker can retrieve the active tab from the currently-focused window (or most recently-focused window, if no Chrome windows are focused). This can usually be thought of as the user's current tab.

```
async function getCurrentTab() {
  let queryOptions = { active: true, lastFocusedWindow: true };
  // `tab` will either be a `tabs.Tab` instance or `undefined`.
  let [tab] = await chrome.tabs.query(queryOptions);
  return tab;
}
```

```
function getCurrentTab(callback) {
  let queryOptions = { active: true, lastFocusedWindow: true };
  chrome.tabs.query(queryOptions, ([tab]) => {
    if (chrome.runtime.lastError) console.error(chrome.runtime.lastError);
    // `tab` will either be a `tabs.Tab` instance or `undefined`.
    callback(tab);
  });
}
```

### Mute the specified tab

This example shows how an extension can toggle the muted state for a given tab.

```
async function toggleMuteState(tabId) {
  const tab = await chrome.tabs.get(tabId);
  const muted = !tab.mutedInfo.muted;
  await chrome.tabs.update(tabId, {muted});
  console.log(`Tab ${tab.id} is ${muted ? "muted" : "unmuted"}`);
}
```

```
function toggleMuteState(tabId) {
  chrome.tabs.get(tabId, async (tab) => {
    let muted = !tab.mutedInfo.muted;
    await chrome.tabs.update(tabId, { muted });
    console.log(`Tab ${tab.id} is ${ muted ? "muted" : "unmuted" }`);
  });
}
```

### Move the current tab to the first position when clicked

This example shows how to move a tab while a drag may or may not be in progress. While this example uses `chrome.tabs.move`, you can use the same waiting pattern for other calls that modify tabs while a drag is in progress.

```
chrome.tabs.onActivated.addListener(moveToFirstPosition);

async function moveToFirstPosition(activeInfo) {
  try {
    await chrome.tabs.move(activeInfo.tabId, {index: 0});
    console.log("Success.");
  } catch (error) {
    if (error == "Error: Tabs cannot be edited right now (user may be dragging a tab).") {
      setTimeout(() => moveToFirstPosition(activeInfo), 50);
    } else {
      console.error(error);
    }
  }
}
```

Important: Using `catch(error)` in a Promise is a way to ensure that an error that otherwise populates `chrome.runtime.lastError` is not unchecked.

```
chrome.tabs.onActivated.addListener(moveToFirstPositionMV2);

function moveToFirstPositionMV2(activeInfo) {
  chrome.tabs.move(activeInfo.tabId, { index: 0 }, () => {
    if (chrome.runtime.lastError) {
      const error = chrome.runtime.lastError;
      if (error == "Error: Tabs cannot be edited right now (user may be dragging a tab).") {
        setTimeout(() => moveToFirstPositionMV2(activeInfo), 50);
      } else {
        console.error(error);
      }
    }
    else {
      console.log("Success.");
    }
  });
}
```

### Pass a message to a selected tab's content script

This example demonstrates how an extension's service worker can communicate with content scripts in specific browser tabs using `tabs.sendMessage()`.

```
function sendMessageToActiveTab(message) {
  const [tab] = await chrome.tabs.query({ active: true, lastFocusedWindow: true });
  const response = await chrome.tabs.sendMessage(tab.id, message);
  // TODO: Do something with the response.
}
```

## Extension examples

For more Tabs API extensions demos, explore any of the following:

* Manifest V2 - Tabs API extensions.
* Manifest V3 - Tabs Manager.

## Types

### MutedInfo

Chrome 46+

The tab's muted state and the reason for the last state change.

#### Properties

* `extensionId`

  `string` optional

  The ID of the extension that changed the muted state. Not set if an extension was not the reason the muted state last changed.
* `muted`

  `boolean`

  Whether the tab is muted (prevented from playing sound). The tab may be muted even if it has not played or is not currently playing sound. Equivalent to whether the `'muted'` audio indicator is showing.
* `reason`

  `MutedInfoReason` optional

  The reason the tab was muted or unmuted. Not set if the tab's mute state has never been changed.

### MutedInfoReason

Chrome 46+

An event that caused a muted state change.

#### Enum

`"user"` A user input action set the muted state.

`"capture"` Tab capture was started, forcing a muted state change.

`"extension"` An extension, identified by the `extensionId` field, set the muted state.

### Tab

#### Properties

* `active`

  `boolean`

  Whether the tab is active in its window. Does not necessarily mean the window is focused.
* `audible`

  `boolean` optional

  Chrome 45+

  Whether the tab has produced sound over the past couple of seconds (but it might not be heard if also muted). Equivalent to whether the `'speaker audio'` indicator is showing.
* `autoDiscardable`

  `boolean`

  Chrome 54+

  Whether the tab can be discarded automatically by the browser when resources are low.
* `discarded`

  `boolean`

  Chrome 54+

  Whether the tab is discarded. A discarded tab is one whose content has been unloaded from memory, but is still visible in the tab strip. Its content is reloaded the next time it is activated.
* `favIconUrl`

  `string` optional

  The URL of the tab's favicon. This property is only present if the extension has the "tabs" permission or has host permissions for the page. It may also be an empty string if the tab is loading.
* `frozen`

  `boolean`

  Chrome 132+

  Whether the tab is frozen. A frozen tab cannot execute tasks, including event handlers or timers. It is visible in the tab strip and its content is loaded in memory. It is unfrozen on activation.
* `groupId`

  `number`

  Chrome 88+

  The ID of the group that the tab belongs to.
* `height`

  `number` optional

  The height of the tab in pixels.
* `highlighted`

  `boolean`

  Whether the tab is highlighted.
* `id`

  `number` optional

  The ID of the tab. Tab IDs are unique within a browser session. Under some circumstances a tab may not be assigned an ID; for example, when querying foreign tabs using the sessions API, in which case a session ID may be present. Tab ID can also be set to `chrome.tabs.TAB_ID_NONE` for apps and devtools windows.
* `incognito`

  `boolean`

  Whether the tab is in an incognito window.
* `index`

  `number`

  The zero-based index of the tab within its window.
* `lastAccessed`

  `number`

  Chrome 121+

  The last time the tab became active in its window as the number of milliseconds since epoch.
* `mutedInfo`

  `MutedInfo` optional

  Chrome 46+

  The tab's muted state and the reason for the last state change.
* `openerTabId`

  `number` optional

  The ID of the tab that opened this tab, if any. This property is only present if the opener tab still exists.
* `pendingUrl`

  `string` optional

  Chrome 79+

  The URL the tab is navigating to, before it has committed. This property is only present if the extension has the "tabs" permission or has host permissions for the page and there is a pending navigation.
* `pinned`

  `boolean`

  Whether the tab is pinned.
* `selected`

  `boolean`

  Deprecated

  Please use `tabs.Tab.highlighted`.

  Whether the tab is selected.
* `sessionId`

  `string` optional

  The session ID used to uniquely identify a tab obtained from the sessions API.
* `status`

  `TabStatus` optional

  The tab's loading status.
* `title`

  `string` optional

  The title of the tab. This property is only present if the extension has the "tabs" permission or has host permissions for the page.
* `url`

  `string` optional

  The last committed URL of the main frame of the tab. This property is only present if the extension has the "tabs" permission or has host permissions for the page. May be an empty string if the tab has not yet committed. See also `Tab.pendingUrl`.
* `width`

  `number` optional

  The width of the tab in pixels.
* `windowId`

  `number`

  The ID of the window that contains the tab.

### TabStatus

Chrome 44+

The tab's loading status.

#### Enum

`"unloaded"`

`"loading"`

`"complete"`

### WindowType

Chrome 44+

The type of window.

#### Enum

`"normal"`

`"popup"`

`"panel"`

`"app"`

`"devtools"`

### ZoomSettings

Defines how zoom changes in a tab are handled and at what scope.

#### Properties

* `defaultZoomFactor`

  `number` optional

  Chrome 43+

  Used to return the default zoom level for the current tab in calls to `tabs.getZoomSettings`.
* `mode`

  `ZoomSettingsMode` optional

  Defines how zoom changes are handled, i.e., which entity is responsible for the actual scaling of the page; defaults to `automatic`.
* `scope`

  `ZoomSettingsScope` optional

  Defines whether zoom changes persist for the page's origin, or only take effect in this tab; defaults to `per-origin` when in `automatic` mode, and `per-tab` otherwise.

### ZoomSettingsMode

Chrome 44+

Defines how zoom changes are handled, i.e., which entity is responsible for the actual scaling of the page; defaults to automatic.

#### Enum

`"automatic"` Zoom changes are handled automatically by the browser.

`"manual"` Overrides the automatic handling of zoom changes. The `onZoomChange` event will still be dispatched, and it is the extension's responsibility to listen for this event and manually scale the page. This mode does not support per-origin zooming, and thus ignores the `scope` zoom setting and assumes per-tab.

`"disabled"` Disables all zooming in the tab. The tab reverts to the default zoom level, and all attempted zoom changes are ignored.

### ZoomSettingsScope

Chrome 44+

Defines whether zoom changes persist for the page's origin, or only take effect in this tab; defaults to per-origin when in automatic mode, and per-tab otherwise.

#### Enum

`"per-origin"` Zoom changes persist in the zoomed page's origin, i.e., all other tabs navigated to that same origin are zoomed as well. Moreover, per-origin zoom changes are saved with the origin, meaning that when navigating to other pages in the same origin, they are all zoomed to the same zoom factor. The `per-origin` scope is only available in the automatic mode.

`"per-tab"` Zoom changes only take effect in this tab, and zoom changes in other tabs do not affect the zooming of this tab. Also, per-tab zoom changes are reset on navigation; navigating a tab always loads pages with their per-origin zoom factors.

## Properties

### MAX_CAPTURE_VISIBLE_TAB_CALLS_PER_SECOND

Chrome 92+

The maximum number of times that `captureVisibleTab` can be called per second. `captureVisibleTab` is expensive and should not be called too often.

#### Value

2

### TAB_ID_NONE

Chrome 46+

An ID that represents the absence of a browser tab.

#### Value

-1

### TAB_INDEX_NONE

Chrome 123+

An index that represents the absence of a tab index in a tab_strip.

#### Value

-1

## Methods

### captureVisibleTab()

Promise

```
chrome.tabs.captureVisibleTab( windowId?: number, options?: ImageDetails, callback?: function, )
```

Captures the visible area of the currently active tab in the specified window. In order to call this method, the extension must have either the `<all_urls>` permission or the `activeTab` permission. In addition to sites that extensions can normally access, this method allows extensions to capture sensitive sites that are otherwise restricted, including `chrome:-scheme` pages, other extensions' pages, and `data:` URLs. These sensitive sites can only be captured with the `activeTab` permission. File URLs may be captured only if the extension has been granted file access.

#### Parameters

* `windowId`

  `number` optional

  The target window. Defaults to the current window.
* `options`

  `ImageDetails` optional
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (dataUrl: string) => void
  ```

  + `dataUrl`

    `string`

    A data URL that encodes an image of the visible area of the captured tab. May be assigned to the `'src'` property of an HTML `img` element for display.

#### Returns

* `Promise<string>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### connect()

```
chrome.tabs.connect( tabId: number, connectInfo?: object, )
```

Connects to the content script(s) in the specified tab. The `runtime.onConnect` event is fired in each content script running in the specified tab for the current extension. For more details, see Content Script Messaging.

#### Parameters

* `tabId`

  `number`
* `connectInfo`

  `object` optional

  + `documentId`

    `string` optional

    Chrome 106+

    Open a port to a specific document identified by `documentId` instead of all frames in the tab.
  + `frameId`

    `number` optional

    Open a port to a specific frame identified by `frameId` instead of all frames in the tab.
  + `name`

    `string` optional

    Is passed into `onConnect` for content scripts that are listening for the connection event.

#### Returns

* `runtime.Port`

  A port that can be used to communicate with the content scripts running in the specified tab. The port's `runtime.Port` event is fired if the tab closes or does not exist.

### create()

Promise

```
chrome.tabs.create( createProperties: object, callback?: function, )
```

Creates a new tab.

#### Parameters

* `createProperties`

  `object`

  + `active`

    `boolean` optional

    Whether the tab should become the active tab in the window. Does not affect whether the window is focused (see windows.update). Defaults to `true`.
  + `index`

    `number` optional

    The position the tab should take in the window. The provided value is clamped to between zero and the number of tabs in the window.
  + `openerTabId`

    `number` optional

    The ID of the tab that opened this tab. If specified, the opener tab must be in the same window as the newly created tab.
  + `pinned`

    `boolean` optional

    Whether the tab should be pinned. Defaults to `false`
  + `selected`

    `boolean` optional

    Deprecated

    Please use `active`.

    Whether the tab should become the selected tab in the window. Defaults to `true`
  + `url`

    `string` optional

    The URL to initially navigate the tab to. Fully-qualified URLs must include a scheme (i.e., `'http://www.google.com'`, not `'www.google.com'`). Relative URLs are relative to the current page within the extension. Defaults to the New Tab Page.
  + `windowId`

    `number` optional

    The window in which to create the new tab. Defaults to the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab: Tab) => void
  ```

  + `tab`

    `Tab`

    The created tab.

#### Returns

* `Promise<Tab>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### detectLanguage()

Promise

```
chrome.tabs.detectLanguage( tabId?: number, callback?: function, )
```

Detects the primary language of the content in a tab.

#### Parameters

* `tabId`

  `number` optional

  Defaults to the active tab of the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (language: string) => void
  ```

  + `language`

    `string`

    An ISO language code such as `en` or `fr`. For a complete list of languages supported by this method, see kLanguageInfoTable. The second to fourth columns are checked and the first non-NULL value is returned, except for Simplified Chinese for which `zh-CN` is returned. For an unknown/undefined language, `und` is returned.

#### Returns

* `Promise<string>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### discard()

Promise Chrome 54+

```
chrome.tabs.discard( tabId?: number, callback?: function, )
```

Discards a tab from memory. Discarded tabs are still visible on the tab strip and are reloaded when activated.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to be discarded. If specified, the tab is discarded unless it is active or already discarded. If omitted, the browser discards the least important tab. This can fail if no discardable tabs exist.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab?: Tab) => void
  ```

  + `tab`

    `Tab` optional

    The discarded tab, if it was successfully discarded; undefined otherwise.

#### Returns

* `Promise<Tab | undefined>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### duplicate()

Promise

```
chrome.tabs.duplicate( tabId: number, callback?: function, )
```

Duplicates a tab.

#### Parameters

* `tabId`

  `number`

  The ID of the tab to duplicate.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab?: Tab) => void
  ```

  + `tab`

    `Tab` optional

    Details about the duplicated tab. The `url`, `pendingUrl`, `title` and `favIconUrl` properties are only included on the `tabs.Tab` object if the extension has the "tabs" permission or has host permissions for the page.

#### Returns

* `Promise<Tab | undefined>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### get()

Promise

```
chrome.tabs.get( tabId: number, callback?: function, )
```

Retrieves details about the specified tab.

#### Parameters

* `tabId`

  `number`
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab: Tab) => void
  ```

  + `tab`

    `Tab`

#### Returns

* `Promise<Tab>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getCurrent()

Promise

```
chrome.tabs.getCurrent( callback?: function, )
```

Gets the tab that this script call is being made from. Returns `undefined` if called from a non-tab context (for example, a background page or popup view).

#### Parameters

* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab?: Tab) => void
  ```

  + `tab`

    `Tab` optional

#### Returns

* `Promise<Tab | undefined>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getZoom()

Promise

```
chrome.tabs.getZoom( tabId?: number, callback?: function, )
```

Gets the current zoom factor of a specified tab.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to get the current zoom factor from; defaults to the active tab of the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (zoomFactor: number) => void
  ```

  + `zoomFactor`

    `number`

    The tab's current zoom factor.

#### Returns

* `Promise<number>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getZoomSettings()

Promise

```
chrome.tabs.getZoomSettings( tabId?: number, callback?: function, )
```

Gets the current zoom settings of a specified tab.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to get the current zoom settings from; defaults to the active tab of the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (zoomSettings: ZoomSettings) => void
  ```

  + `zoomSettings`

    `ZoomSettings`

    The tab's current zoom settings.

#### Returns

* `Promise<ZoomSettings>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### goBack()

Promise Chrome 72+

```
chrome.tabs.goBack( tabId?: number, callback?: function, )
```

Go back to the previous page, if one is available.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to navigate back; defaults to the selected tab of the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### goForward()

Promise Chrome 72+

```
chrome.tabs.goForward( tabId?: number, callback?: function, )
```

Go foward to the next page, if one is available.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to navigate forward; defaults to the selected tab of the current window.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### group()

Promise Chrome 88+

```
chrome.tabs.group( options: object, callback?: function, )
```

Adds one or more tabs to a specified group, or if no group is specified, adds the given tabs to a newly created group.

#### Parameters

* `options`

  `object`

  + `createProperties`

    `object` optional

    Configurations for creating a group. Cannot be used if `groupId` is already specified.

    - `windowId`

      `number` optional

      The window of the new group. Defaults to the current window.
  + `groupId`

    `number` optional

    The ID of the group to add the tabs to. If not specified, a new group will be created.
  + `tabIds`

    `number | [number, ...number[]]`

    The tab ID or list of tab IDs to add to the specified group.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (groupId: number) => void
  ```

  + `groupId`

    `number`

    The ID of the group that the tabs were added to.

#### Returns

* `Promise<number>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### highlight()

Promise

```
chrome.tabs.highlight( highlightInfo: object, callback?: function, )
```

Highlights the given tabs and focuses on the first of group. Will appear to do nothing if the specified tab is currently active.

#### Parameters

* `highlightInfo`

  `object`

  + `tabs`

    `number | number[]`

    One or more tab indices to highlight.
  + `windowId`

    `number` optional

    The window that contains the tabs.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (window: Window) => void
  ```

  + `window`

    `Window`

    Contains details about the window whose tabs were highlighted.

#### Returns

* `Promise<windows.Window>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### move()

Promise

```
chrome.tabs.move( tabIds: number | number[], moveProperties: object, callback?: function, )
```

Moves one or more tabs to a new position within its window, or to a new window. Note that tabs can only be moved to and from normal (`window.type === "normal"`) windows.

#### Parameters

* `tabIds`

  `number | number[]`

  The tab ID or list of tab IDs to move.
* `moveProperties`

  `object`

  + `index`

    `number`

    The position to move the window to. Use -1 to place the tab at the end of the window.
  + `windowId`

    `number` optional

    Defaults to the window the tab is currently in.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tabs: Tab | Tab[]) => void
  ```

  + `tabs`

    `Tab | Tab[]`

    Details about the moved tabs.

#### Returns

* `Promise<Tab | Tab[]>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### query()

Promise

```
chrome.tabs.query( queryInfo: object, callback?: function, )
```

Gets all tabs that have the specified properties, or all tabs if no properties are specified.

#### Parameters

* `queryInfo`

  `object`

  + `active`

    `boolean` optional

    Whether the tabs are active in their windows.
  + `audible`

    `boolean` optional

    Chrome 45+

    Whether the tabs are audible.
  + `autoDiscardable`

    `boolean` optional

    Chrome 54+

    Whether the tabs can be discarded automatically by the browser when resources are low.
  + `currentWindow`

    `boolean` optional

    Whether the tabs are in the current window.
  + `discarded`

    `boolean` optional

    Chrome 54+

    Whether the tabs are discarded. A discarded tab is one whose content has been unloaded from memory, but is still visible in the tab strip. Its content is reloaded the next time it is activated.
  + `frozen`

    `boolean` optional

    Chrome 132+

    Whether the tabs are frozen. A frozen tab cannot execute tasks, including event handlers or timers. It is visible in the tab strip and its content is loaded in memory. It is unfrozen on activation.
  + `groupId`

    `number` optional

    Chrome 88+

    The ID of the group that the tabs are in, or `tabGroups.TAB_GROUP_ID_NONE` for ungrouped tabs.
  + `highlighted`

    `boolean` optional

    Whether the tabs are highlighted.
  + `index`

    `number` optional

    The position of the tabs within their windows.
  + `lastFocusedWindow`

    `boolean` optional

    Whether the tabs are in the last focused window.
  + `muted`

    `boolean` optional

    Chrome 45+

    Whether the tabs are muted.
  + `pinned`

    `boolean` optional

    Whether the tabs are pinned.
  + `status`

    `TabStatus` optional

    The tab loading status.
  + `title`

    `string` optional

    Match page titles against a pattern. This property is ignored if the extension does not have the "tabs" permission or host permissions for the page.
  + `url`

    `string | string[]` optional

    Match tabs against one or more URL patterns. Fragment identifiers are not matched. This property is ignored if the extension does not have the "tabs" permission or host permissions for the page.
  + `windowId`

    `number` optional

    The ID of the parent window, or `windows.WINDOW_ID_CURRENT` for the current window.
  + `windowType`

    `WindowType` optional

    The type of window the tabs are in.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (result: Tab[]) => void
  ```

  + `result`

    `Tab[]`

#### Returns

* `Promise<Tab[]>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### reload()

Promise

```
chrome.tabs.reload( tabId?: number, reloadProperties?: object, callback?: function, )
```

Reload a tab.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to reload; defaults to the selected tab of the current window.
* `reloadProperties`

  `object` optional

  + `bypassCache`

    `boolean` optional

    Whether to bypass local caching. Defaults to `false`.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### remove()

Promise

```
chrome.tabs.remove( tabIds: number | number[], callback?: function, )
```

Closes one or more tabs.

#### Parameters

* `tabIds`

  `number | number[]`

  The tab ID or list of tab IDs to close.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### sendMessage()

Promise

```
chrome.tabs.sendMessage( tabId: number, message: any, options?: object, callback?: function, )
```

Sends a single message to the content script(s) in the specified tab, with an optional callback to run when a response is sent back. The `runtime.onMessage` event is fired in each content script running in the specified tab for the current extension.

#### Parameters

* `tabId`

  `number`
* `message`

  `any`

  The message to send. This message should be a JSON-ifiable object.
* `options`

  `object` optional

  + `documentId`

    `string` optional

    Chrome 106+

    Send a message to a specific document identified by `documentId` instead of all frames in the tab.
  + `frameId`

    `number` optional

    Send a message to a specific frame identified by `frameId` instead of all frames in the tab.
* `callback`

  `function` optional

  Chrome 99+

  The callback parameter looks like:

  ```
  (response: any) => void
  ```

  + `response`

    `any`

    The JSON response object sent by the handler of the message. If an error occurs while connecting to the specified tab, the callback is called with no arguments and `runtime.lastError` is set to the error message.

#### Returns

* `Promise<any>`

  Chrome 99+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setZoom()

Promise

```
chrome.tabs.setZoom( tabId?: number, zoomFactor: number, callback?: function, )
```

Zooms a specified tab.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to zoom; defaults to the active tab of the current window.
* `zoomFactor`

  `number`

  The new zoom factor. A value of 0 sets the tab to its current default zoom factor. Values greater than 0 specify a (possibly non-default) zoom factor for the tab.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### setZoomSettings()

Promise

```
chrome.tabs.setZoomSettings( tabId?: number, zoomSettings: ZoomSettings, callback?: function, )
```

Sets the zoom settings for a specified tab, which define how zoom changes are handled. These settings are reset to defaults upon navigating the tab.

#### Parameters

* `tabId`

  `number` optional

  The ID of the tab to change the zoom settings for; defaults to the active tab of the current window.
* `zoomSettings`

  `ZoomSettings`

  Defines how zoom changes are handled and at what scope.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### ungroup()

Promise Chrome 88+

```
chrome.tabs.ungroup( tabIds: number | [number, ...number[]], callback?: function, )
```

Removes one or more tabs from their respective groups. If any groups become empty, they are deleted.

#### Parameters

* `tabIds`

  `number | [number, ...number[]]`

  The tab ID or list of tab IDs to remove from their respective groups.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### update()

Promise

```
chrome.tabs.update( tabId?: number, updateProperties: object, callback?: function, )
```

Modifies the properties of a tab. Properties that are not specified in `updateProperties` are not modified.

#### Parameters

* `tabId`

  `number` optional

  Defaults to the selected tab of the current window.
* `updateProperties`

  `object`

  + `active`

    `boolean` optional

    Whether the tab should be active. Does not affect whether the window is focused (see windows.update).
  + `autoDiscardable`

    `boolean` optional

    Chrome 54+

    Whether the tab should be discarded automatically by the browser when resources are low.
  + `highlighted`

    `boolean` optional

    Adds or removes the tab from the current selection.
  + `muted`

    `boolean` optional

    Chrome 45+

    Whether the tab should be muted.
  + `openerTabId`

    `number` optional

    The ID of the tab that opened this tab. If specified, the opener tab must be in the same window as this tab.
  + `pinned`

    `boolean` optional

    Whether the tab should be pinned.
  + `selected`

    `boolean` optional

    Deprecated

    Please use `highlighted`.

    Whether the tab should be selected.
  + `url`

    `string` optional

    A URL to navigate the tab to. JavaScript URLs are not supported; use `scripting.executeScript` instead.
* `callback`

  `function` optional

  The callback parameter looks like:

  ```
  (tab?: Tab) => void
  ```

  + `tab`

    `Tab` optional

    Details about the updated tab. The `url`, `pendingUrl`, `title` and `favIconUrl` properties are only included on the `tabs.Tab` object if the extension has the "tabs" permission or has host permissions for the page.

#### Returns

* `Promise<Tab | undefined>`

  Chrome 88+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onActivated

```
chrome.tabs.onActivated.addListener( callback: function, )
```

Fires when the active tab in a window changes. Note that the tab's URL may not be set at the time this event fired, but you can listen to `onUpdated` events so as to be notified when a URL is set.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (activeInfo: object) => void
  ```

  + `activeInfo`

    `object`

    - `tabId`

      `number`

      The ID of the tab that has become active.
    - `windowId`

      `number`

      The ID of the window the active tab changed inside of.

### onAttached

```
chrome.tabs.onAttached.addListener( callback: function, )
```

Fired when a tab is attached to a window; for example, because it was moved between windows.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tabId: number, attachInfo: object) => void
  ```

  + `tabId`

    `number`
  + `attachInfo`

    `object`

    - `newPosition`

      `number`
    - `newWindowId`

      `number`

### onCreated

```
chrome.tabs.onCreated.addListener( callback: function, )
```

Fired when a tab is created. Note that the tab's URL and tab group membership may not be set at the time this event is fired, but you can listen to `onUpdated` events so as to be notified when a URL is set or the tab is added to a tab group.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tab: Tab) => void
  ```

  + `tab`

    `Tab`

### onDetached

```
chrome.tabs.onDetached.addListener( callback: function, )
```

Fired when a tab is detached from a window; for example, because it was moved between windows.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tabId: number, detachInfo: object) => void
  ```

  + `tabId`

    `number`
  + `detachInfo`

    `object`

    - `oldPosition`

      `number`
    - `oldWindowId`

      `number`

### onHighlighted

```
chrome.tabs.onHighlighted.addListener( callback: function, )
```

Fired when the highlighted or selected tabs in a window changes.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (highlightInfo: object) => void
  ```

  + `highlightInfo`

    `object`

    - `tabIds`

      `number[]`

      All highlighted tabs in the window.
    - `windowId`

      `number`

      The window whose tabs changed.

### onMoved

```
chrome.tabs.onMoved.addListener( callback: function, )
```

Fired when a tab is moved within a window. Only one move event is fired, representing the tab the user directly moved. Move events are not fired for the other tabs that must move in response to the manually-moved tab. This event is not fired when a tab is moved between windows; for details, see `tabs.onDetached`.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tabId: number, moveInfo: object) => void
  ```

  + `tabId`

    `number`
  + `moveInfo`

    `object`

    - `fromIndex`

      `number`
    - `toIndex`

      `number`
    - `windowId`

      `number`

### onRemoved

```
chrome.tabs.onRemoved.addListener( callback: function, )
```

Fired when a tab is closed.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tabId: number, removeInfo: object) => void
  ```

  + `tabId`

    `number`
  + `removeInfo`

    `object`

    - `isWindowClosing`

      `boolean`

      True when the tab was closed because its parent window was closed.
    - `windowId`

      `number`

      The window whose tab is closed.

### onReplaced

```
chrome.tabs.onReplaced.addListener( callback: function, )
```

Fired when a tab is replaced with another tab due to prerendering or instant.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (addedTabId: number, removedTabId: number) => void
  ```

  + `addedTabId`

    `number`
  + `removedTabId`

    `number`

### onUpdated

```
chrome.tabs.onUpdated.addListener( callback: function, )
```

Fired when a tab is updated.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (tabId: number, changeInfo: object, tab: Tab) => void
  ```

  + `tabId`

    `number`
  + `changeInfo`

    `object`

    - `audible`

      `boolean` optional

      Chrome 45+

      The tab's new audible state.
    - `autoDiscardable`

      `boolean` optional

      Chrome 54+

      The tab's new auto-discardable state.
    - `discarded`

      `boolean` optional

      Chrome 54+

      The tab's new discarded state.
    - `favIconUrl`

      `string` optional

      The tab's new favicon URL.
    - `frozen`

      `boolean` optional

      Chrome 132+

      The tab's new frozen state.
    - `groupId`

      `number` optional

      Chrome 88+

      The tab's new group.
    - `mutedInfo`

      `MutedInfo` optional

      Chrome 46+

      The tab's new muted state and the reason for the change.
    - `pinned`

      `boolean` optional

      The tab's new pinned state.
    - `status`

      `TabStatus` optional

      The tab's loading status.
    - `title`

      `string` optional

      Chrome 48+

      The tab's new title.
    - `url`

      `string` optional

      The tab's URL if it has changed.
  + `tab`

    `Tab`

### onZoomChange

```
chrome.tabs.onZoomChange.addListener( callback: function, )
```

Fired when a tab is zoomed.

#### Parameters

* `callback`

  `function`

  The callback parameter looks like:

  ```
  (ZoomChangeInfo: object) => void
  ```

  + `ZoomChangeInfo`

    `object`

    - `newZoomFactor`

      `number`
    - `oldZoomFactor`

      `number`
    - `tabId`

      `number`
    - `zoomSettings`

      `ZoomSettings`

</rewritten_file> 

===

---
title: chrome.topSites
url: https://developer.chrome.com/docs/extensions/reference/api/topSites
---

# chrome.topSites

## Description

Use the `chrome.topSites` API to access the top sites (i.e. most visited sites) that are displayed on the new tab page. These do not include shortcuts customized by the user.

## Permissions

`topSites`

You must declare the "`topSites`" permission in your extension's manifest to use this API.

```json
{ "name": "My extension", ... "permissions": [ "topSites", ], ... }
```

## Examples

To try this API, install the `topSites` API example from the `chrome-extension-samples` repository.

## Types

### `MostVisitedURL`

An object encapsulating a most visited URL, such as the default shortcuts on the new tab page.

#### Properties

* `title`

  string

  The title of the page
* `url`

  string

  The most visited URL.

## Methods

### `get()`

Promise

```js
chrome.topSites.get( callback?: function, )
```

Gets a list of top sites.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (data: MostVisitedURL[]) => void
  ```

  + `data`

    `MostVisitedURL[]`

#### Returns

* `Promise<MostVisitedURL[]>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.tts
url: https://developer.chrome.com/docs/extensions/reference/api/tts
---

# chrome.tts

## Description

Use the `chrome.tts` API to play synthesized text-to-speech (TTS). See also the related `ttsEngine` API, which allows an extension to implement a speech engine.

Chrome provides this capability on Windows (using SAPI 5), Mac OS X, and ChromeOS, using speech synthesis capabilities provided by the operating system. On all platforms, the user can install extensions that register themselves as alternative speech engines.

## Permissions

`tts`

## Concepts and usage

### Generate speech

Call `speak()` from your extension to speak. For example:

```js
chrome.tts.speak('Hello, world.');
```

To stop speaking immediately, just call `stop()`:

```js
chrome.tts.stop();
```

You can provide options that control various properties of the speech, such as its rate, pitch, and more. For example:

```js
chrome.tts.speak('Hello, world.', {'rate': 2.0});
```

It's also a good idea to specify the language so that a synthesizer supporting that language (and regional dialect, if applicable) is chosen.

```js
chrome.tts.speak('Hello, world.', {'lang': 'en-US', 'rate': 2.0});
```

By default, each call to `speak()` interrupts any ongoing speech and speaks immediately. To determine if a call would be interrupting anything, you can call `isSpeaking()`. In addition, you can use the `enqueue` option to cause this utterance to be added to a queue of utterances that will be spoken when the current utterance has finished.

```js
chrome.tts.speak('Speak this first.');
chrome.tts.speak( 'Speak this next, when the first sentence is done.', {'enqueue': true});
```

A complete description of all options can be found under `tts.speak()`. Not all speech engines will support all options.

To catch errors and make sure you're calling `speak()` correctly, pass a callback function that takes no arguments. Inside the callback, check `runtime.lastError` to see if there were any errors.

```js
chrome.tts.speak( utterance, options, function() { if (chrome.runtime.lastError) { console.log('Error: ' + chrome.runtime.lastError.message); } } );
```

The callback returns right away, before the engine has started generating speech. The purpose of the callback is to alert you to syntax errors in your use of the TTS API, not to catch all possible errors that might occur in the process of synthesizing and outputting speech. To catch these errors too, you need to use an event listener, described in the next section.

### Listen to events

To get more real-time information about the status of synthesized speech, pass an event listener in the options to `speak()`, like this:

```js
chrome.tts.speak( utterance, { onEvent: function(event) { console.log('Event ' + event.type + ' at position ' + event.charIndex); if (event.type == 'error') { console.log('Error: ' + event.errorMessage); } } }, callback );
```

Each event includes an event type, the character index of the current speech relative to the utterance, and for error events, an optional error message. The event types are:

* '`start`': The engine has started speaking the utterance.
* '`word`': A word boundary was reached. Use `event.charIndex` to determine the current speech position.
* '`sentence`': A sentence boundary was reached. Use `event.charIndex` to determine the current speech position.
* '`marker`': An SSML marker was reached. Use `event.charIndex` to determine the current speech position.
* '`end`': The engine has finished speaking the utterance.
* '`interrupted`': This utterance was interrupted by another call to `speak()` or `stop()` and did not finish.
* '`cancelled`': This utterance was queued, but then cancelled by another call to `speak()` or `stop()` and never began to speak at all.
* '`error`': An engine-specific error occurred and this utterance cannot be spoken. Check `event.errorMessage` for details.

Four of the event types鈥?`end`', '`interrupted`', '`cancelled`', and '`error`'鈥攁re final. After one of those events is received, this utterance will no longer speak and no new events from this utterance will be received.

Some voices may not support all event types, and some voices may not send any events at all. If you don't want to use a voice unless it sends certain events, pass the events you require in the `requiredEventTypes` member of the options object, or use `getVoices()` to choose a voice that meets your requirements. Both are described in what follows.

### SSML markup

Utterances used in this API may include markup using the Speech Synthesis Markup Language (SSML). If you use SSML, the first argument to `speak()` should be a complete SSML document with an XML header and a top-level `<speak>` tag, not a document fragment.

For example:

```js
chrome.tts.speak( '<?xml version="1.0"?>' + '<speak>' + ' The <emphasis>second</emphasis> ' + ' word of this sentence was emphasized.' + '</speak>' );
```

Not all speech engines will support all SSML tags, and some may not support SSML at all, but all engines are required to ignore any SSML they don't support and to still speak the underlying text.

### Choose a voice

By default, Chrome chooses the most appropriate voice for each utterance you want to speak, based on the language. On most Windows, Mac OS X, and ChromeOS systems, speech synthesis provided by the operating system should be able to speak any text in at least one language. Some users may have a variety of voices available, though, from their operating system and from speech engines implemented by other Chrome extensions. In those cases, you can implement custom code to choose the appropriate voice, or to present the user with a list of choices.

To get a list of all voices, call `getVoices()` and pass it a function that receives an array of `TtsVoice` objects as its argument:

```js
chrome.tts.getVoices( function(voices) { for (var i = 0; i < voices.length; i++) { console.log('Voice ' + i + ':'); console.log('  name: ' + voices[i].voiceName); console.log('  lang: ' + voices[i].lang); console.log('  extension id: ' + voices[i].extensionId); console.log('  event types: ' + voices[i].eventTypes); } } );
```

## Types

### `EventType`

Chrome 54+

#### Enum

"`start`"

"`end`"

"`word`"

"`sentence`"

"`marker`"

"`interrupted`"

"`cancelled`"

"`error`"

"`pause`"

"`resume`"

### `TtsEvent`

An event from the TTS engine to communicate the status of an utterance.

#### Properties

* `charIndex`

  number optional

  The index of the current character in the utterance. For word events, the event fires at the end of one word and before the beginning of the next. The `charIndex` represents a point in the text at the beginning of the next word to be spoken.
* `errorMessage`

  string optional

  The error description, if the event type is error.
* `length`

  number optional

  Chrome 74+

  The length of the next part of the utterance. For example, in a word event, this is the length of the word which will be spoken next. It will be set to -1 if not set by the speech engine.
* `type`

  `EventType`

  The type can be `start` as soon as speech has started, `word` when a word boundary is reached, `sentence` when a sentence boundary is reached, `marker` when an SSML mark element is reached, `end` when the end of the utterance is reached, `interrupted` when the utterance is stopped or interrupted before reaching the end, `cancelled` when it's removed from the queue before ever being synthesized, or `error` when any other error occurs. When pausing speech, a `pause` event is fired if a particular utterance is paused in the middle, and `resume` if an utterance resumes speech. Note that `pause` and `resume` events may not fire if speech is paused in-between utterances.

### `TtsOptions`

Chrome 77+

The speech options for the TTS engine.

#### Properties

* `desiredEventTypes`

  string[] optional

  The TTS event types that you are interested in listening to. If missing, all event types may be sent.
* `enqueue`

  boolean optional

  If true, enqueues this utterance if TTS is already in progress. If false (the default), interrupts any current speech and flushes the speech queue before speaking this new utterance.
* `extensionId`

  string optional

  The extension ID of the speech engine to use, if known.
* `gender`

  `VoiceGender` optional

  Deprecated since Chrome 77

  Gender is deprecated and will be ignored.

  Gender of voice for synthesized speech.
* `lang`

  string optional

  The language to be used for synthesis, in the form language-region. Examples: '`en`', '`en-US`', '`en-GB`', '`zh-CN`'.
* `pitch`

  number optional

  Speaking pitch between 0 and 2 inclusive, with 0 being lowest and 2 being highest. 1.0 corresponds to a voice's default pitch.
* `rate`

  number optional

  Speaking rate relative to the default rate for this voice. 1.0 is the default rate, normally around 180 to 220 words per minute. 2.0 is twice as fast, and 0.5 is half as fast. Values below 0.1 or above 10.0 are strictly disallowed, but many voices will constrain the minimum and maximum rates further鈥攆or example a particular voice may not actually speak faster than 3 times normal even if you specify a value larger than 3.0.
* `requiredEventTypes`

  string[] optional

  The TTS event types the voice must support.
* `voiceName`

  string optional

  The name of the voice to use for synthesis. If empty, uses any available voice.
* `volume`

  number optional

  Speaking volume between 0 and 1 inclusive, with 0 being lowest and 1 being highest, with a default of 1.0.
* `onEvent`

  void optional

  This function is called with events that occur in the process of speaking the utterance.

  The `onEvent` function looks like:

  ```js
  (event: TtsEvent) => {...}
  ```

  + `event`

    `TtsEvent`

    The update event from the text-to-speech engine indicating the status of this utterance.

### `TtsVoice`

A description of a voice available for speech synthesis.

#### Properties

* `eventTypes`

  `EventType[]` optional

  All of the callback event types that this voice is capable of sending.
* `extensionId`

  string optional

  The ID of the extension providing this voice.
* `gender`

  `VoiceGender` optional

  Deprecated since Chrome 70

  Gender is deprecated and will be ignored.

  This voice's gender.
* `lang`

  string optional

  The language that this voice supports, in the form language-region. Examples: '`en`', '`en-US`', '`en-GB`', '`zh-CN`'.
* `remote`

  boolean optional

  If true, the synthesis engine is a remote network resource. It may be higher latency and may incur bandwidth costs.
* `voiceName`

  string optional

  The name of the voice.

### `VoiceGender`

Chrome 54+ Deprecated since Chrome 70

Gender is deprecated and is ignored.

#### Enum

"`male`"

"`female`"

## Methods

### `getVoices()`

Promise

```js
chrome.tts.getVoices( callback?: function, )
```

Gets an array of all available voices.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (voices: TtsVoice[]) => void
  ```

  + `voices`

    `TtsVoice[]`

    Array of `tts.TtsVoice` objects representing the available voices for speech synthesis.

#### Returns

* `Promise<TtsVoice[]>`

  Chrome 101+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `isSpeaking()`

Promise

```js
chrome.tts.isSpeaking( callback?: function, )
```

Checks whether the engine is currently speaking. On Mac OS X, the result is true whenever the system speech engine is speaking, even if the speech wasn't initiated by Chrome.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (speaking: boolean) => void
  ```

  + `speaking`

    boolean

    True if speaking, false otherwise.

#### Returns

* `Promise<boolean>`

  Chrome 101+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `pause()`

```js
chrome.tts.pause()
```

Pauses speech synthesis, potentially in the middle of an utterance. A call to `resume` or `stop` will un-pause speech.

### `resume()`

```js
chrome.tts.resume()
```

If speech was paused, resumes speaking where it left off.

### `speak()`

Promise

```js
chrome.tts.speak( utterance: string, options?: TtsOptions, callback?: function, )
```

Speaks text using a text-to-speech engine.

#### Parameters

* `utterance`

  string

  The text to speak, either plain text or a complete, well-formed SSML document. Speech engines that do not support SSML will strip away the tags and speak the text. The maximum length of the text is 32,768 characters.
* `options`

  `TtsOptions` optional

  The speech options.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 101+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `stop()`

```js
chrome.tts.stop()
```

Stops any current speech and flushes the queue of any pending utterances. In addition, if speech was paused, it will now be un-paused for the next call to `speak`.

## Events

### `onVoicesChanged`

Chrome 124+

```js
chrome.tts.onVoicesChanged.addListener( callback: function, )
```

Called when the list of `tts.TtsVoice` that would be returned by `getVoices` has changed.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  () => void
  ``` 

===

---
title: chrome.ttsEngine
url: https://developer.chrome.com/docs/extensions/reference/api/ttsEngine
---

# chrome.ttsEngine

## Description

Use the `chrome.ttsEngine` API to implement a text-to-speech(TTS) engine using an extension. If your extension registers using this API, it will receive events containing an utterance to be spoken and other parameters when any extension or Chrome App uses the `tts` API to generate speech. Your extension can then use any available web technology to synthesize and output the speech, and send events back to the calling function to report the status.

## Permissions

`ttsEngine`

## Concepts and usage

An extension can register itself as a speech engine. By doing so, it can intercept some or all calls to functions such as `tts.speak()` and `tts.stop()` and provide an alternate implementation. Extensions are free to use any available web technology to provide speech, including streaming audio from a server, HTML5 audio. An extension could even do something different with the utterances, like display closed captions in a popup or send them as log messages to a remote server.

To implement a TTS engine, an extension must declare the "`ttsEngine`" permission and then declare all voices it provides in the extension manifest, like this:

```json
{ "name": "My TTS Engine", "version": "1.0", "permissions": ["ttsEngine"], "tts_engine": { "voices": [ { "voice_name": "Alice", "lang": "en-US", "event_types": ["start", "marker", "end"] }, { "voice_name": "Pat", "lang": "en-US", "event_types": ["end"] } ] }, "background": { "page": "background.html", "persistent": false } }
```

An extension can specify any number of voices.

The `voice_name` parameter is required. The name should be descriptive enough that it identifies the name of the voice and the engine used. In the unlikely event that two extensions register voices with the same name, a client can specify the ID of the extension that should do the synthesis.

The `lang` parameter is optional, but highly recommended. Almost always, a voice can synthesize speech in just a single language. When an engine supports more than one language, it can easily register a separate voice for each language. Under rare circumstances where a single voice can handle more than one language, it's easiest to just list two separate voices and handle them using the same logic internally. However, if you want to create a voice that will handle utterances in any language, leave out the `lang` parameter from your extension's manifest.

Finally, the `event_types` parameter is required if the engine can send events to update the client on the progress of speech synthesis. At a minimum, supporting the '`end`' event type to indicate when speech is finished is highly recommended, otherwise Chrome cannot schedule queued utterances.

Once loaded, an extension can replace the list of declared voices by calling `chrome.ttsEngine.updateVoices`. (Note that the parameters used in the programatic call to `updateVoices` are in camel case: e.g., `voiceName`, unlike the manifest file which uses `voice_name`.)

Note: If your TTS engine does not support the '`end`' event type, Chrome cannot queue utterances because it has no way of knowing when your utterance has finished. To help mitigate this, Chrome passes an additional boolean `enqueue` option to your engine's `onSpeak` handler, giving you the option of implementing your own queueing. This is discouraged because then clients are unable to queue utterances that should get spoken by different speech engines.

The possible event types that you can send correspond to the event types that the `speak()` method receives:

* '`start`': The engine has started speaking the utterance.
* '`word`': A word boundary was reached. Use `event.charIndex` to determine the current speech position.
* '`sentence`': A sentence boundary was reached. Use `event.charIndex` to determine the current speech position.
* '`marker`': An SSML marker was reached. Use `event.charIndex` to determine the current speech position.
* '`end`': The engine has finished speaking the utterance.
* '`error`': An engine-specific error occurred and this utterance cannot be spoken. Pass more information in `event.errorMessage`.

The '`interrupted`' and '`cancelled`' events are not sent by the speech engine; they are generated automatically by Chrome.

Text-to-speech clients can get the voice information from your extension's manifest by calling `tts.getVoices`, assuming you've registered speech event listeners as described below.

### Handle speech events

To generate speech at the request of clients, your extension must register listeners for both `onSpeak` and `onStop`, like this:

```js
const speakListener = (utterance, options, sendTtsEvent) => { sendTtsEvent({type: 'start', charIndex: 0}) // (start speaking) sendTtsEvent({type: 'end', charIndex: utterance.length}) }; const stopListener = () => { // (stop all speech) }; chrome.ttsEngine.onSpeak.addListener(speakListener); chrome.ttsEngine.onStop.addListener(stopListener);
```

Caution: If your extension does not register listeners for both `onSpeak` and `onStop`, it will not intercept any speech calls, regardless of what is in the manifest.

The decision of whether or not to send a given speech request to an extension is based solely on whether the extension supports the given voice parameters in its manifest and has registered listeners for `onSpeak` and `onStop`. In other words, there's no way for an extension to receive a speech request and dynamically decide whether to handle it.

## Types

### `AudioBuffer`

Chrome 92+

Parameters containing an audio buffer and associated data.

#### Properties

* `audioBuffer`

  `ArrayBuffer`

  The audio buffer from the text-to-speech engine. It should have length exactly `audioStreamOptions.bufferSize` and encoded as mono, at `audioStreamOptions.sampleRate`, and as linear pcm, 32-bit signed float i.e. the `Float32Array` type in javascript.
* `charIndex`

  number optional

  The character index associated with this audio buffer.
* `isLastBuffer`

  boolean optional

  True if this audio buffer is the last for the text being spoken.

### `AudioStreamOptions`

Chrome 92+

Contains the audio stream format expected to be produced by an engine.

#### Properties

* `bufferSize`

  number

  The number of samples within an audio buffer.
* `sampleRate`

  number

  The sample rate expected in an audio buffer.

### `LanguageInstallStatus`

Chrome 132+

The install status of a voice.

#### Enum

"`notInstalled`"

"`installing`"

"`installed`"

"`failed`"

### `LanguageStatus`

Chrome 132+

Install status of a language.

#### Properties

* `error`

  string optional

  Detail about installation failures. Optionally populated if the language failed to install.
* `installStatus`

  `LanguageInstallStatus`

  Installation status.
* `lang`

  string

  Language string in the form of language code-region code, where the region may be omitted. Examples are `en`, `en-AU`, `zh-CH`.

### `LanguageUninstallOptions`

Chrome 132+

Options for uninstalling a given language.

#### Properties

* `uninstallImmediately`

  boolean

  True if the TTS client wants the language to be immediately uninstalled. The engine may choose whether or when to uninstall the language, based on this parameter and the requestor information. If false, it may use other criteria, such as recent usage, to determine when to uninstall.

### `SpeakOptions`

Chrome 92+

Options specified to the `tts.speak()` method.

#### Properties

* `gender`

  `VoiceGender` optional

  Deprecated since Chrome 92

  Gender is deprecated and will be ignored.

  Gender of voice for synthesized speech.
* `lang`

  string optional

  The language to be used for synthesis, in the form language-region. Examples: '`en`', '`en-US`', '`en-GB`', '`zh-CN`'.
* `pitch`

  number optional

  Speaking pitch between 0 and 2 inclusive, with 0 being lowest and 2 being highest. 1.0 corresponds to this voice's default pitch.
* `rate`

  number optional

  Speaking rate relative to the default rate for this voice. 1.0 is the default rate, normally around 180 to 220 words per minute. 2.0 is twice as fast, and 0.5 is half as fast. This value is guaranteed to be between 0.1 and 10.0, inclusive. When a voice does not support this full range of rates, don't return an error. Instead, clip the rate to the range the voice supports.
* `voiceName`

  string optional

  The name of the voice to use for synthesis.
* `volume`

  number optional

  Speaking volume between 0 and 1 inclusive, with 0 being lowest and 1 being highest, with a default of 1.0.

### `TtsClient`

Chrome 131+

Identifier for the client requesting status.

#### Properties

* `id`

  string

  Client making a language management request. For an extension, this is the unique extension ID. For Chrome features, this is the human-readable name of the feature.
* `source`

  `TtsClientSource`

  Type of requestor.

### `TtsClientSource`

Chrome 131+

Type of requestor.

#### Enum

"`chromefeature`"

"`extension`"

### `VoiceGender`

Chrome 54+ Deprecated since Chrome 70

Gender is deprecated and will be ignored.

#### Enum

"`male`"

"`female`"

## Methods

### `updateLanguage()`

Chrome 132+

```js
chrome.ttsEngine.updateLanguage( status: LanguageStatus, )
```

Called by an engine when a language install is attempted, and when a language is uninstalled. Also called in response to a status request from a client. When a voice is installed or uninstalled, the engine should also call `ttsEngine.updateVoices` to register the voice.

#### Parameters

* `status`

  `LanguageStatus`

  The install status of the language.

### `updateVoices()`

Chrome 66+

```js
chrome.ttsEngine.updateVoices( voices: TtsVoice[], )
```

Called by an engine to update its list of voices. This list overrides any voices declared in this extension's manifest.

#### Parameters

* `voices`

  `TtsVoice[]`

  Array of `tts.TtsVoice` objects representing the available voices for speech synthesis.

## Events

### `onInstallLanguageRequest`

Chrome 131+

```js
chrome.ttsEngine.onInstallLanguageRequest.addListener( callback: function, )
```

Fired when a TTS client requests to install a new language. The engine should attempt to download and install the language, and call `ttsEngine.updateLanguage` with the result. On success, the engine should also call `ttsEngine.updateVoices` to register the newly available voices.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestor: TtsClient, lang: string) => void
  ```

  + `requestor`

    `TtsClient`
  + `lang`

    string

### `onLanguageStatusRequest`

Chrome 132+

```js
chrome.ttsEngine.onLanguageStatusRequest.addListener( callback: function, )
```

Fired when a TTS client requests the install status of a language.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestor: TtsClient, lang: string) => void
  ```

  + `requestor`

    `TtsClient`
  + `lang`

    string

### `onPause`

```js
chrome.ttsEngine.onPause.addListener( callback: function, )
```

Optional: if an engine supports the pause event, it should pause the current utterance being spoken, if any, until it receives a resume event or stop event. Note that a stop event should also clear the paused state.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  () => void
  ```

### `onResume`

```js
chrome.ttsEngine.onResume.addListener( callback: function, )
```

Optional: if an engine supports the pause event, it should also support the resume event, to continue speaking the current utterance, if any. Note that a stop event should also clear the paused state.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  () => void
  ```

### `onSpeak`

```js
chrome.ttsEngine.onSpeak.addListener( callback: function, )
```

Called when the user makes a call to `tts.speak()` and one of the voices from this extension's manifest is the first to match the options object.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (utterance: string, options: SpeakOptions, sendTtsEvent: function) => void
  ```

  + `utterance`

    string
  + `options`

    `SpeakOptions`
  + `sendTtsEvent`

    function

    The `sendTtsEvent` parameter looks like:

    ```js
    (event: tts.TtsEvent) => void
    ```

    - `event`

      `tts.TtsEvent`

      The event from the text-to-speech engine indicating the status of this utterance.

### `onSpeakWithAudioStream`

Chrome 92+

```js
chrome.ttsEngine.onSpeakWithAudioStream.addListener( callback: function, )
```

Called when the user makes a call to `tts.speak()` and one of the voices from this extension's manifest is the first to match the options object. Differs from `ttsEngine.onSpeak` in that Chrome provides audio playback services and handles dispatching tts events.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (utterance: string, options: SpeakOptions, audioStreamOptions: AudioStreamOptions, sendTtsAudio: function, sendError: function) => void
  ```

  + `utterance`

    string
  + `options`

    `SpeakOptions`
  + `audioStreamOptions`

    `AudioStreamOptions`
  + `sendTtsAudio`

    function

    The `sendTtsAudio` parameter looks like:

    ```js
    (audioBufferParams: AudioBuffer) => void
    ```

    - `audioBufferParams`

      `AudioBuffer`

      Parameters containing an audio buffer and associated data.
  + `sendError`

    function

    Chrome 94+

    The `sendError` parameter looks like:

    ```js
    (errorMessage?: string) => void
    ```

    - `errorMessage`

      string optional

      A string describing the error.

### `onStop`

```js
chrome.ttsEngine.onStop.addListener( callback: function, )
```

Fired when a call is made to `tts.stop` and this extension may be in the middle of speaking. If an extension receives a call to `onStop` and speech is already stopped, it should do nothing (not raise an error). If speech is in the paused state, this should cancel the paused state.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  () => void
  ```

### `onUninstallLanguageRequest`

Chrome 132+

```js
chrome.ttsEngine.onUninstallLanguageRequest.addListener( callback: function, )
```

Fired when a TTS client indicates a language is no longer needed.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestor: TtsClient, lang: string, uninstallOptions: LanguageUninstallOptions) => void
  ```

  + `requestor`

    `TtsClient`
  + `lang`

    string
  + `uninstallOptions`

    `LanguageUninstallOptions`

===

---
title: chrome.types
url: https://developer.chrome.com/docs/extensions/reference/api/types
---

# chrome.types

## Description

The `chrome.types` API contains type declarations for Chrome.

## Chrome settings

The `ChromeSetting` type provides a common set of functions (`get()`, `set()`, and `clear()`) as well as an event publisher (`onChange`) for settings of the Chrome browser. The proxy settings examples demonstrate how these functions are intended to be used.

### Scope and lifecycle

Chrome distinguishes between three different scopes of browser settings:

regular
:   Settings set in the regular scope apply to regular browser windows and are inherited by incognito windows if they are not overwritten. These settings are stored to disk and remain in place until they are cleared by the governing extension, or the governing extension is disabled or uninstalled.

incognito\_persistent
:   Settings set in the `incognito_persistent` scope apply only to incognito windows. For these, they override regular settings. These settings are stored to disk and remain in place until they are cleared by the governing extension, or the governing extension is disabled or uninstalled.

incognito\_session\_only
:   Settings set in the `incognito_session_only` scope apply only to incognito windows. For these, they override regular and `incognito_persistent` settings. These settings are not stored to disk and are cleared when the last incognito window is closed. They can only be set when at least one incognito window is open.

### Precedence

Chrome manages settings on different layers. The following list describes the layers that may influence the effective settings, in increasing order of precedence.

1. System settings provided by the operating system
2. Command-line parameters
3. Settings provided by extensions
4. Policies

As the list implies, policies might overrule any changes that you specify with your extension. You can use the `get()` function to determine whether your extension is capable of providing a setting or whether this setting would be overridden.

As discussed previously, Chrome allows using different settings for regular windows and incognito windows. The following example illustrates the behavior. Assume that no policy overrides the settings and that an extension can set settings for regular windows (R) and settings for incognito windows (I).

* If only (R) is set, these settings are effective for both regular and incognito windows.
* If only (I) is set, these settings are effective for only incognito windows. Regular windows use the settings determined by the lower layers (command-line options and system settings).
* If both (R) and (I) are set, the respective settings are used for regular and incognito windows.

If two or more extensions want to set the same setting to different values, the extension installed most recently takes precedence over the other extensions. If the most recently installed extension sets only (I), the settings of regular windows can be defined by previously installed extensions.

The effective value of a setting is the one that results from considering the precedence rules. It is used by Chrome.

## Types

### `ChromeSetting`

An interface that allows access to a Chrome browser setting. See `accessibilityFeatures` for an example.

#### Properties

* `onChange`

  `Event<functionvoidvoid>`

  Fired after the setting changes.

  The `onChange.addListener` function looks like:

  ```js
  (callback: function) => {...}
  ```

  + `callback`

    function

    The callback parameter looks like:

    ```js
    (details: object) => void
    ```

    - `details`

      object

      * `incognitoSpecific`

        boolean optional

        Whether the value that has changed is specific to the incognito session. This property will only be present if the user has enabled the extension in incognito mode.
      * `levelOfControl`

        `LevelOfControl`

        The level of control of the setting.
      * `value`

        T

        The value of the setting after the change.
* `clear`

  void

  Promise

  Clears the setting, restoring any default value.

  The `clear` function looks like:

  ```js
  (details: object, callback?: function) => {...}
  ```

  + `details`

    object

    Which setting to clear.

    - `scope`

      `ChromeSettingScope` optional

      Where to clear the setting (default: regular).
  + `callback`

    function optional

    The callback parameter looks like:

    ```js
    () => void
    ```

  + returns

    `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `get`

  void

  Promise

  Gets the value of a setting.

  The `get` function looks like:

  ```js
  (details: object, callback?: function) => {...}
  ```

  + `details`

    object

    Which setting to consider.

    - `incognito`

      boolean optional

      Whether to return the value that applies to the incognito session (default false).
  + `callback`

    function optional

    The callback parameter looks like:

    ```js
    (details: object) => void
    ```

    - `details`

      object

      Details of the currently effective value.

      * `incognitoSpecific`

        boolean optional

        Whether the effective value is specific to the incognito session. This property will only be present if the incognito property in the details parameter of `get()` was true.
      * `levelOfControl`

        `LevelOfControl`

        The level of control of the setting.
      * `value`

        T

        The value of the setting.

  + returns

    `Promise<object>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.
* `set`

  void

  Promise

  Sets the value of a setting.

  The `set` function looks like:

  ```js
  (details: object, callback?: function) => {...}
  ```

  + `details`

    object

    Which setting to change.

    - `scope`

      `ChromeSettingScope` optional

      Where to set the setting (default: regular).
    - `value`

      T

      The value of the setting. Note that every setting has a specific value type, which is described together with the setting. An extension should not set a value of a different type.
  + `callback`

    function optional

    The callback parameter looks like:

    ```js
    () => void
    ```

  + returns

    `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `ChromeSettingScope`

Chrome 44+

The scope of the `ChromeSetting`. One of

* `regular`: setting for the regular profile (which is inherited by the incognito profile if not overridden elsewhere),
* `regular\_only`: setting for the regular profile only (not inherited by the incognito profile),
* `incognito\_persistent`: setting for the incognito profile that survives browser restarts (overrides regular preferences),
* `incognito\_session\_only`: setting for the incognito profile that can only be set during an incognito session and is deleted when the incognito session ends (overrides regular and `incognito_persistent` preferences).

#### Enum

"`regular`"

"`regular\_only`"

"`incognito\_persistent`"

"`incognito\_session\_only`"

### `LevelOfControl`

Chrome 44+

One of

* `not\_controllable`: cannot be controlled by any extension
* `controlled\_by\_other\_extensions`: controlled by extensions with higher precedence
* `controllable\_by\_this\_extension`: can be controlled by this extension
* `controlled\_by\_this\_extension`: controlled by this extension

#### Enum

"`not\_controllable`"

"`controlled\_by\_other\_extensions`"

"`controllable\_by\_this\_extension`"

"`controlled\_by\_this\_extension`" 

===

---
title: chrome.userScripts
url: https://developer.chrome.com/docs/extensions/reference/api/userScripts
---

# chrome.userScripts

## Description

Use the `userScripts` API to execute user scripts in the User Scripts context.

## Permissions

`userScripts`

To use the User Scripts API, `chrome.userScripts`, add the "`userScripts`" permission to your `manifest.json` and "`host_permissions`" for sites you want to run scripts on.

```json
{ "name": "User script test extension", "manifest_version": 3, "minimum_chrome_version": "120", "permissions": [ "userScripts" ], "host_permissions": [ "*://example.com/*" ] }
```

## Availability

Chrome 120+ MV3+

## Concepts and usage

A user script is a snippet of code injected into a web page to modify its appearance or behavior. Unlike other extension features, such as Content Scripts and the `chrome.scripting` API, the User Scripts API lets you run arbitrary code. This API is required for extensions that run scripts provided by the user that cannot be shipped as part of your extension package.

### Developer mode for extension users

As an extension developer, you already have Developer mode enabled in your installation of Chrome. For user script extensions, your users will also need to enable developer mode. Here are instructions that you can copy and paste into your own documentation.

1. Go to the Extensions page by entering `chrome://extensions` in a new tab. (By design `chrome://` URLs are not linkable.)
2. Enable Developer Mode by clicking the toggle switch next to Developer mode.

   Extensions page (`chrome://extensions`)

You can determine if developer mode is enabled by checking whether `chrome.userScripts` throws an error. For example:

```js
function isUserScriptsAvailable() { try { // Property access which throws if developer mode is not enabled. chrome.userScripts; return true; } catch { // Not available. return false; } }
```

### Work in isolated worlds

Both user and content scripts can run in an isolated world or in the main world. An isolated world is an execution environment that isn't accessible to a host page or other extensions. This lets a user script change its JavaScript environment without affecting the host page or other extensions' user and content scripts. Conversely, user scripts (and content scripts) are not visible to the host page or the user and content scripts of other extensions. Scripts running in the main world are accessible to host pages and other extensions and are visible to host pages and to other extensions. To select the world, pass "`USER_SCRIPT`" or "`MAIN`" when calling `userScripts.register()`.

To configure a content security policy for the `USER_SCRIPT` world, call `userScripts.configureWorld()`:

```js
chrome.userScripts.configureWorld({ csp: "script-src 'self'" });
```

### Messaging

Like content scripts and offscreen documents, user scripts communicate with other parts of an extension using messaging (meaning they can call `runtime.sendMessage()` and `runtime.connect()` as any other part of an extension would). However, they're received using dedicated event handlers (meaning, they don't use `onMessage` or `onConnect`). These handlers are called `runtime.onUserScriptMessage` and `runtime.onUserScriptConnect`. Dedicated handlers make it easier to identify messages from user scripts, which are a less-trusted context.

Before sending a message, you must call `configureWorld()` with the messaging argument set to true. Note that both the `csp` and `messaging` arguments can be passed at the same time.

```js
chrome.userScripts.configureWorld({ messaging: true });
```

### Extension updates

User scripts are cleared when an extension updates. You can add them back by running code in the `runtime.onInstalled` event handler in the extension service worker. Respond only to the "`update`" reason passed to the event callback.

## Example

This example is from the `userScript` sample in our samples repository.

### Register a script

The following example shows a basic call to `register()`. The first argument is an array of objects defining the scripts to be registered. There are more options than are shown here.

```js
chrome.userScripts.register([{ id: 'test', matches: ['*://*/*'], js: [{code: 'alert("Hi!")'}] }]);
```

## Types

### `ExecutionWorld`

The JavaScript world for a user script to execute within.

#### Enum

"`MAIN`" Specifies the execution environment of the DOM, which is the execution environment shared with the host page's JavaScript.

"`USER_SCRIPT`" Specifies the execution environment that is specific to user scripts and is exempt from the page's CSP.

### `InjectionResult`

Chrome 135+

#### Properties

* `documentId`

  string

  The document associated with the injection.
* `error`

  string optional

  The error, if any. `error` and `result` are mutually exclusive.
* `frameId`

  number

  The frame associated with the injection.
* `result`

  any optional

  The result of the script execution.

### `InjectionTarget`

Chrome 135+

#### Properties

* `allFrames`

  boolean optional

  Whether the script should inject into all frames within the tab. Defaults to false. This must not be true if `frameIds` is specified.
* `documentIds`

  string[] optional

  The IDs of specific `documentIds` to inject into. This must not be set if `frameIds` is set.
* `frameIds`

  number[] optional

  The IDs of specific frames to inject into.
* `tabId`

  number

  The ID of the tab into which to inject.

### `RegisteredUserScript`

#### Properties

* `allFrames`

  boolean optional

  If true, it will inject into all frames, even if the frame is not the top-most frame in the tab. Each frame is checked independently for URL requirements; it will not inject into child frames if the URL requirements are not met. Defaults to false, meaning that only the top frame is matched.
* `excludeGlobs`

  string[] optional

  Specifies wildcard patterns for pages this user script will NOT be injected into.
* `excludeMatches`

  string[] optional

  Excludes pages that this user script would otherwise be injected into. See Match Patterns for more details on the syntax of these strings.
* `id`

  string

  The ID of the user script specified in the API call. This property must not start with a '`_`' as it's reserved as a prefix for generated script IDs.
* `includeGlobs`

  string[] optional

  Specifies wildcard patterns for pages this user script will be injected into.
* `js`

  `ScriptSource[]` optional

  The list of `ScriptSource` objects defining sources of scripts to be injected into matching pages. This property must be specified for `${ref:register}`, and when specified it must be a non-empty array.
* `matches`

  string[] optional

  Specifies which pages this user script will be injected into. See Match Patterns for more details on the syntax of these strings. This property must be specified for `${ref:register}`.
* `runAt`

  `RunAt` optional

  Specifies when JavaScript files are injected into the web page. The preferred and default value is `document_idle`.
* `world`

  `ExecutionWorld` optional

  The JavaScript execution environment to run the script in. The default is ``USER_SCRIPT``.
* `worldId`

  string optional

  Chrome 133+

  Specifies the user script world ID to execute in. If omitted, the script will execute in the default user script world. Only valid if `world` is omitted or is `USER_SCRIPT`. Values with leading underscores (`_`) are reserved.

### `ScriptSource`

#### Properties

* `code`

  string optional

  A string containing the JavaScript code to inject. Exactly one of `file` or `code` must be specified.
* `file`

  string optional

  The path of the JavaScript file to inject relative to the extension's root directory. Exactly one of `file` or `code` must be specified.

### `UserScriptFilter`

#### Properties

* `ids`

  string[] optional

  `getScripts` only returns scripts with the IDs specified in this list.

### `UserScriptInjection`

Chrome 135+

#### Properties

* `injectImmediately`

  boolean optional

  Whether the injection should be triggered in the target as soon as possible. Note that this is not a guarantee that injection will occur prior to page load, as the page may have already loaded by the time the script reaches the target.
* `js`

  `ScriptSource[]`

  The list of `ScriptSource` objects defining sources of scripts to be injected into the target.
* `target`

  `InjectionTarget`

  Details specifying the target into which to inject the script.
* `world`

  `ExecutionWorld` optional

  The JavaScript "world" to run the script in. The default is `USER_SCRIPT`.
* `worldId`

  string optional

  Specifies the user script world ID to execute in. If omitted, the script will execute in the default user script world. Only valid if `world` is omitted or is `USER_SCRIPT`. Values with leading underscores (`_`) are reserved.

### `WorldProperties`

#### Properties

* `csp`

  string optional

  Specifies the world csp. The default is the `ISOLATED` world csp.
* `messaging`

  boolean optional

  Specifies whether messaging APIs are exposed. The default is false.
* `worldId`

  string optional

  Chrome 133+

  Specifies the ID of the specific user script world to update. If not provided, updates the properties of the default user script world. Values with leading underscores (`_`) are reserved.

## Methods

### `configureWorld()`

Promise

```js
chrome.userScripts.configureWorld( properties: WorldProperties, callback?: function, )
```

Configures the ``USER_SCRIPT`` execution environment.

#### Parameters

* `properties`

  `WorldProperties`

  Contains the user script world configuration.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `execute()`

Promise Chrome 135+

```js
chrome.userScripts.execute( injection: UserScriptInjection, callback?: function, )
```

Injects a script into a target context. By default, the script will be run at `document_idle`, or immediately if the page has already loaded. If the `injectImmediately` property is set, the script will inject without waiting, even if the page has not finished loading. If the script evaluates to a promise, the browser will wait for the promise to settle and return the resulting value.

#### Parameters

* `injection`

  `UserScriptInjection`
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (result: InjectionResult[]) => void
  ```

  + `result`

    `InjectionResult[]`

#### Returns

* `Promise<InjectionResult[]>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getScripts()`

Promise

```js
chrome.userScripts.getScripts( filter?: UserScriptFilter, callback?: function, )
```

Returns all dynamically-registered user scripts for this extension.

#### Parameters

* `filter`

  `UserScriptFilter` optional

  If specified, this method returns only the user scripts that match it.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (scripts: RegisteredUserScript[]) => void
  ```

  + `scripts`

    `RegisteredUserScript[]`

#### Returns

* `Promise<RegisteredUserScript[]>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getWorldConfigurations()`

Promise Chrome 133+

```js
chrome.userScripts.getWorldConfigurations( callback?: function, )
```

Retrieves all registered world configurations.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (worlds: WorldProperties[]) => void
  ```

  + `worlds`

    `WorldProperties[]`

#### Returns

* `Promise<WorldProperties[]>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `register()`

Promise

```js
chrome.userScripts.register( scripts: RegisteredUserScript[], callback?: function, )
```

Registers one or more user scripts for this extension.

#### Parameters

* `scripts`

  `RegisteredUserScript[]`

  Contains a list of user scripts to be registered.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `resetWorldConfiguration()`

Promise Chrome 133+

```js
chrome.userScripts.resetWorldConfiguration( worldId?: string, callback?: function, )
```

Resets the configuration for a user script world. Any scripts that inject into the world with the specified ID will use the default world configuration.

#### Parameters

* `worldId`

  string optional

  The ID of the user script world to reset. If omitted, resets the default world's configuration.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `unregister()`

Promise

```js
chrome.userScripts.unregister( filter?: UserScriptFilter, callback?: function, )
```

Unregisters all dynamically-registered user scripts for this extension.

#### Parameters

* `filter`

  `UserScriptFilter` optional

  If specified, this method unregisters only the user scripts that match it.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `update()`

Promise

```js
chrome.userScripts.update( scripts: RegisteredUserScript[], callback?: function, )
```

Updates one or more user scripts for this extension.

#### Parameters

* `scripts`

  `RegisteredUserScript[]`

  Contains a list of user scripts to be updated. A property is only updated for the existing script if it is specified in this object. If there are errors during script parsing/file validation, or if the IDs specified do not correspond to a fully registered script, then no scripts are updated.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.vpnProvider
url: https://developer.chrome.com/docs/extensions/reference/api/vpnProvider
---

# chrome.vpnProvider

Important: This API works only on ChromeOS.

## Description

Use the `chrome.vpnProvider` API to implement a VPN client.

## Permissions

`vpnProvider`

## Availability

Chrome 43+ ChromeOS only

## Concepts and usage

Typical usage of `chrome.vpnProvider` is as follows:

* Create VPN configurations by calling `createConfig()`. A VPN configuration is a persistent entry shown to the user in a ChromeOS UI. The user can select a VPN configuration from a list and connect to it or disconnect from it.
* Add listeners to the `onPlatformMessage`, `onPacketReceived`, and `onConfigRemoved` events.
* When the user connects to the VPN configuration, `onPlatformMessage` will be received with the message "`connected`". The period between the "`connected`" and "`disconnected`" messages is called a "VPN session". In this time period, the extension that receives the message is said to own the VPN session.
* Initiate connection to the VPN server and start the VPN client.
* Set the Parameters of the connection by calling `setParameters()`.
* Notify the connection state as "`connected`" by calling `notifyConnectionStateChanged()`.
* When the steps previous are completed without errors, a virtual tunnel is created to the network stack of ChromeOS. IP packets can be sent through the tunnel by calling `sendPacket()` and any packets originating on the ChromeOS device will be received using the `onPacketReceived` event handler.
* When the user disconnects from the VPN configuration, `onPlatformMessage` will be fired with the message "`disconnected`".
* If the VPN configuration is no longer necessary, it can be destroyed by calling `destroyConfig()`.

## Types

### `Parameters`

#### Properties

* `address`

  string

  IP address for the VPN interface in CIDR notation. IPv4 is currently the only supported mode.
* `broadcastAddress`

  string optional

  Broadcast address for the VPN interface. (default: deduced from IP address and mask)
* `dnsServers`

  string[]

  A list of IPs for the DNS servers.
* `domainSearch`

  string[] optional

  A list of search domains. (default: no search domain)
* `exclusionList`

  string[]

  Exclude network traffic to the list of IP blocks in CIDR notation from the tunnel. This can be used to bypass traffic to and from the VPN server. When many rules match a destination, the rule with the longest matching prefix wins. Entries that correspond to the same CIDR block are treated as duplicates. Such duplicates in the collated (`exclusionList` + `inclusionList`) list are eliminated and the exact duplicate entry that will be eliminated is undefined.
* `inclusionList`

  string[]

  Include network traffic to the list of IP blocks in CIDR notation to the tunnel. This parameter can be used to set up a split tunnel. By default no traffic is directed to the tunnel. Adding the entry "`0.0.0.0/0`" to this list gets all the user traffic redirected to the tunnel. When many rules match a destination, the rule with the longest matching prefix wins. Entries that correspond to the same CIDR block are treated as duplicates. Such duplicates in the collated (`exclusionList` + `inclusionList`) list are eliminated and the exact duplicate entry that will be eliminated is undefined.
* `mtu`

  string optional

  MTU setting for the VPN interface. (default: 1500 bytes)
* `reconnect`

  string optional

  Chrome 51+

  Whether or not the VPN extension implements auto-reconnection.

  If true, the `linkDown`, `linkUp`, `linkChanged`, `suspend`, and `resume` platform messages will be used to signal the respective events. If false, the system will forcibly disconnect the VPN if the network topology changes, and the user will need to reconnect manually. (default: false)

  This property is new in Chrome 51; it will generate an exception in earlier versions. `try/catch` can be used to conditionally enable the feature based on browser support.

### `PlatformMessage`

The enum is used by the platform to notify the client of the VPN session status.

#### Enum

"`connected`" Indicates that the VPN configuration connected.

"`disconnected`" Indicates that the VPN configuration disconnected.

"`error`" Indicates that an error occurred in VPN connection, for example a timeout. A description of the error is given as the error argument to `onPlatformMessage`.

"`linkDown`" Indicates that the default physical network connection is down.

"`linkUp`" Indicates that the default physical network connection is back up.

"`linkChanged`" Indicates that the default physical network connection changed, e.g. wifi->mobile.

"`suspend`" Indicates that the OS is preparing to suspend, so the VPN should drop its connection. The extension is not guaranteed to receive this event prior to suspending.

"`resume`" Indicates that the OS has resumed and the user has logged back in, so the VPN should try to reconnect.

### `UIEvent`

The enum is used by the platform to indicate the event that triggered `onUIEvent`.

#### Enum

"`showAddDialog`" Requests that the VPN client show the add configuration dialog box to the user.

"`showConfigureDialog`" Requests that the VPN client show the configuration settings dialog box to the user.

### `VpnConnectionState`

The enum is used by the VPN client to inform the platform of its current state. This helps provide meaningful messages to the user.

#### Enum

"`connected`" Specifies that VPN connection was successful.

"`failure`" Specifies that VPN connection has failed.

## Methods

### `createConfig()`

Promise

```js
chrome.vpnProvider.createConfig( name: string, callback?: function, )
```

Creates a new VPN configuration that persists across multiple login sessions of the user.

#### Parameters

* `name`

  string

  The name of the VPN configuration.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (id: string) => void
  ```

  + `id`

    string

    A unique ID for the created configuration, or undefined on failure.

#### Returns

* `Promise<string>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `destroyConfig()`

Promise

```js
chrome.vpnProvider.destroyConfig( id: string, callback?: function, )
```

Destroys a VPN configuration created by the extension.

#### Parameters

* `id`

  string

  ID of the VPN configuration to destroy.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `notifyConnectionStateChanged()`

Promise

```js
chrome.vpnProvider.notifyConnectionStateChanged( state: VpnConnectionState, callback?: function, )
```

Notifies the VPN session state to the platform. This will succeed only when the VPN session is owned by the extension.

#### Parameters

* `state`

  `VpnConnectionState`

  The VPN session state of the VPN client.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `sendPacket()`

Promise

```js
chrome.vpnProvider.sendPacket( data: ArrayBuffer, callback?: function, )
```

Sends an IP packet through the tunnel created for the VPN session. This will succeed only when the VPN session is owned by the extension.

#### Parameters

* `data`

  `ArrayBuffer`

  The IP packet to be sent to the platform.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `setParameters()`

Promise

```js
chrome.vpnProvider.setParameters( parameters: Parameters, callback?: function, )
```

Sets the parameters for the VPN session. This should be called immediately after "`connected`" is received from the platform. This will succeed only when the VPN session is owned by the extension.

#### Parameters

* `parameters`

  `Parameters`

  The parameters for the VPN session.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onConfigCreated`

```js
chrome.vpnProvider.onConfigCreated.addListener( callback: function, )
```

Triggered when a configuration is created by the platform for the extension.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (id: string, name: string, data: object) => void
  ```

  + `id`

    string
  + `name`

    string
  + `data`

    object

### `onConfigRemoved`

```js
chrome.vpnProvider.onConfigRemoved.addListener( callback: function, )
```

Triggered when a configuration created by the extension is removed by the platform.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (id: string) => void
  ```

  + `id`

    string

### `onPacketReceived`

```js
chrome.vpnProvider.onPacketReceived.addListener( callback: function, )
```

Triggered when an IP packet is received via the tunnel for the VPN session owned by the extension.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (data: ArrayBuffer) => void
  ```

  + `data`

    `ArrayBuffer`

### `onPlatformMessage`

```js
chrome.vpnProvider.onPlatformMessage.addListener( callback: function, )
```

Triggered when a message is received from the platform for a VPN configuration owned by the extension.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (id: string, message: PlatformMessage, error: string) => void
  ```

  + `id`

    string
  + `message`

    `PlatformMessage`
  + `error`

    string

### `onUIEvent`

```js
chrome.vpnProvider.onUIEvent.addListener( callback: function, )
```

Triggered when there is a UI event for the extension. UI events are signals from the platform that indicate to the app that a UI dialog needs to be shown to the user.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (event: UIEvent, id?: string) => void
  ```

  + `event`

    `UIEvent`
  + `id`

    string optional 

===

---
title: chrome.wallpaper
url: https://developer.chrome.com/docs/extensions/reference/api/wallpaper
---

# chrome.wallpaper

Important: This API works only on ChromeOS.

## Description

Use the `chrome.wallpaper` API to change the ChromeOS wallpaper.

## Permissions

`wallpaper`

You must declare the "`wallpaper`" permission in the app's manifest to use the wallpaper API. For example:

```json
{ "name": "My extension", ... "permissions": [ "wallpaper" ], ... }
```

## Availability

Chrome 43+ ChromeOS only

## Examples

For example, to set the wallpaper as the image at `https://example.com/a_file.png`, you can call `chrome.wallpaper.setWallpaper` this way:

```js
chrome.wallpaper.setWallpaper( { 'url': 'https://example.com/a_file.jpg', 'layout': 'CENTER_CROPPED', 'filename': 'test_wallpaper' }, function() {} );
```

## Types

### `WallpaperLayout`

Chrome 44+

The supported wallpaper layouts.

#### Enum

"`STRETCH`"

"`CENTER`"

"`CENTER_CROPPED`"

## Methods

### `setWallpaper()`

Promise

```js
chrome.wallpaper.setWallpaper( details: object, callback?: function, )
```

Sets wallpaper to the image at url or wallpaperData with the specified layout

#### Parameters

* `details`

  object

  + `data`

    `ArrayBuffer` optional

    The jpeg or png encoded wallpaper image as an `ArrayBuffer`.
  + `filename`

    string

    The file name of the saved wallpaper.
  + `layout`

    `WallpaperLayout`

    The supported wallpaper layouts.
  + `thumbnail`

    boolean optional

    True if a 128x60 thumbnail should be generated. Layout and ratio are not supported yet.
  + `url`

    string optional

    The URL of the wallpaper to be set (can be relative).
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (thumbnail?: ArrayBuffer) => void
  ```

  + `thumbnail`

    `ArrayBuffer` optional

    The jpeg encoded wallpaper thumbnail. It is generated by resizing the wallpaper to 128x60.

#### Returns

* `Promise<ArrayBuffer | undefined>`

  Chrome 96+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback. 

===

---
title: chrome.webAuthenticationProxy
url: https://developer.chrome.com/docs/extensions/reference/api/webAuthenticationProxy
---

# chrome.webAuthenticationProxy

## Description

The `chrome.webAuthenticationProxy` API lets remote desktop software running on a remote host intercept Web Authentication API (WebAuthn) requests in order to handle them on a local client.

## Permissions

`webAuthenticationProxy`

## Availability

Chrome 115+ MV3+

## Types

### `CreateRequest`

#### Properties

* `requestDetailsJson`

  string

  The `PublicKeyCredentialCreationOptions` passed to `navigator.credentials.create()`, serialized as a JSON string. The serialization format is compatible with `PublicKeyCredential.parseCreationOptionsFromJSON()`.
* `requestId`

  number

  An opaque identifier for the request.

### `CreateResponseDetails`

#### Properties

* `error`

  `DOMExceptionDetails` optional

  The `DOMException` yielded by the remote request, if any.
* `requestId`

  number

  The `requestId` of the `CreateRequest`.
* `responseJson`

  string optional

  The `PublicKeyCredential`, yielded by the remote request, if any, serialized as a JSON string by calling href="https://w3c.github.io/webauthn/#dom-publickeycredential-tojson"> `PublicKeyCredential.toJSON()`.

### `DOMExceptionDetails`

#### Properties

* `message`

  string
* `name`

  string

### `GetRequest`

#### Properties

* `requestDetailsJson`

  string

  The `PublicKeyCredentialRequestOptions` passed to `navigator.credentials.get()`, serialized as a JSON string. The serialization format is compatible with `PublicKeyCredential.parseRequestOptionsFromJSON()`.
* `requestId`

  number

  An opaque identifier for the request.

### `GetResponseDetails`

#### Properties

* `error`

  `DOMExceptionDetails` optional

  The `DOMException` yielded by the remote request, if any.
* `requestId`

  number

  The `requestId` of the `CreateRequest`.
* `responseJson`

  string optional

  The `PublicKeyCredential`, yielded by the remote request, if any, serialized as a JSON string by calling href="https://w3c.github.io/webauthn/#dom-publickeycredential-tojson"> `PublicKeyCredential.toJSON()`.

### `IsUvpaaRequest`

#### Properties

* `requestId`

  number

  An opaque identifier for the request.

### `IsUvpaaResponseDetails`

#### Properties

* `isUvpaa`

  boolean
* `requestId`

  number

## Methods

### `attach()`

Promise

```js
chrome.webAuthenticationProxy.attach( callback?: function, )
```

Makes this extension the active Web Authentication API request proxy.

Remote desktop extensions typically call this method after detecting attachment of a remote session to this host. Once this method returns without error, regular processing of WebAuthn requests is suspended, and events from this extension API are raised.

This method fails with an error if a different extension is already attached.

The attached extension must call `detach()` once the remote desktop session has ended in order to resume regular WebAuthn request processing. Extensions automatically become detached if they are unloaded.

Refer to the `onRemoteSessionStateChange` event for signaling a change of remote session attachment from a native application to to the (possibly suspended) extension.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (error?: string) => void
  ```

  + `error`

    string optional

#### Returns

* `Promise<string | undefined>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `completeCreateRequest()`

Promise

```js
chrome.webAuthenticationProxy.completeCreateRequest( details: CreateResponseDetails, callback?: function, )
```

Reports the result of a `navigator.credentials.create()` call. The extension must call this for every `onCreateRequest` event it has received, unless the request was canceled (in which case, an `onRequestCanceled` event is fired).

#### Parameters

* `details`

  `CreateResponseDetails`
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `completeGetRequest()`

Promise

```js
chrome.webAuthenticationProxy.completeGetRequest( details: GetResponseDetails, callback?: function, )
```

Reports the result of a `navigator.credentials.get()` call. The extension must call this for every `onGetRequest` event it has received, unless the request was canceled (in which case, an `onRequestCanceled` event is fired).

#### Parameters

* `details`

  `GetResponseDetails`
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `completeIsUvpaaRequest()`

Promise

```js
chrome.webAuthenticationProxy.completeIsUvpaaRequest( details: IsUvpaaResponseDetails, callback?: function, )
```

Reports the result of a `PublicKeyCredential.isUserVerifyingPlatformAuthenticator()` call. The extension must call this for every `onIsUvpaaRequest` event it has received.

#### Parameters

* `details`

  `IsUvpaaResponseDetails`
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  () => void
  ```

#### Returns

* `Promise<void>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `detach()`

Promise

```js
chrome.webAuthenticationProxy.detach( callback?: function, )
```

Removes this extension from being the active Web Authentication API request proxy.

This method is typically called when the extension detects that a remote desktop session was terminated. Once this method returns, the extension ceases to be the active Web Authentication API request proxy.

Refer to the `onRemoteSessionStateChange` event for signaling a change of remote session attachment from a native application to to the (possibly suspended) extension.

#### Parameters

* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (error?: string) => void
  ```

  + `error`

    string optional

#### Returns

* `Promise<string | undefined>`

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onCreateRequest`

```js
chrome.webAuthenticationProxy.onCreateRequest.addListener( callback: function, )
```

Fires when a WebAuthn `navigator.credentials.create()` call occurs. The extension must supply a response by calling `completeCreateRequest()` with the `requestId` from `requestInfo`.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestInfo: CreateRequest) => void
  ```

  + `requestInfo`

    `CreateRequest`

### `onGetRequest`

```js
chrome.webAuthenticationProxy.onGetRequest.addListener( callback: function, )
```

Fires when a WebAuthn `navigator.credentials.get()` call occurs. The extension must supply a response by calling `completeGetRequest()` with the `requestId` from `requestInfo`

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestInfo: GetRequest) => void
  ```

  + `requestInfo`

    `GetRequest`

### `onIsUvpaaRequest`

```js
chrome.webAuthenticationProxy.onIsUvpaaRequest.addListener( callback: function, )
```

Fires when a `PublicKeyCredential.isUserVerifyingPlatformAuthenticatorAvailable()` call occurs. The extension must supply a response by calling `completeIsUvpaaRequest()` with the `requestId` from `requestInfo`

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestInfo: IsUvpaaRequest) => void
  ```

  + `requestInfo`

    `IsUvpaaRequest`

### `onRemoteSessionStateChange`

```js
chrome.webAuthenticationProxy.onRemoteSessionStateChange.addListener( callback: function, )
```

A native application associated with this extension can cause this event to be fired by writing to a file with a name equal to the extension's ID in a directory named `WebAuthenticationProxyRemoteSessionStateChange` inside the default user data directory

The contents of the file should be empty. I.e., it is not necessary to change the contents of the file in order to trigger this event.

The native host application may use this event mechanism to signal a possible remote session state change (i.e. from detached to attached, or vice versa) while the extension service worker is possibly suspended. In the handler for this event, the extension can call the `attach()` or `detach()` API methods accordingly.

The event listener must be registered synchronously at load time.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  () => void
  ```

### `onRequestCanceled`

```js
chrome.webAuthenticationProxy.onRequestCanceled.addListener( callback: function, )
```

Fires when a `onCreateRequest` or `onGetRequest` event is canceled (because the WebAuthn request was aborted by the caller, or because it timed out). When receiving this event, the extension should cancel processing of the corresponding request on the client side. Extensions cannot complete a request once it has been canceled.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (requestId: number) => void
  ```

  + `requestId`

    number 

===

---
title: chrome.webNavigation
url: https://developer.chrome.com/docs/extensions/reference/api/webNavigation
---

# chrome.webNavigation

## Description

Use the `chrome.webNavigation` API to receive notifications about the status of navigation requests in-flight.

## Permissions

`webNavigation`

All `chrome.webNavigation` methods and events require you to declare the "`webNavigation`" permission in the extension manifest. For example:

```json
{ "name": "My extension", ... "permissions": [ "webNavigation" ], ... }
```

## Concepts and usage

### Event order

For a navigation that is successfully completed, events are fired in the following order:

```
onBeforeNavigate -> onCommitted -> [onDOMContentLoaded] -> onCompleted
```

Any error that occurs during the process results in an `onErrorOccurred` event. For a specific navigation, there are no further events fired after `onErrorOccurred`.

If a navigating frame contains subframes, its `onCommitted` is fired before any of its children's `onBeforeNavigate`; while `onCompleted` is fired after all of its children's `onCompleted`.

If the reference fragment of a frame is changed, a `onReferenceFragmentUpdated` event is fired. This event can fire any time after `onDOMContentLoaded`, even after `onCompleted`.

If the history API is used to modify the state of a frame (e.g. using `history.pushState()`, a `onHistoryStateUpdated` event is fired. This event can fire any time after `onDOMContentLoaded`.

If a navigation restored a page from the Back Forward Cache, the `onDOMContentLoaded` event won't fire. The event is not fired because the content has already completed load when the page was first visited.

If a navigation was triggered using Chrome Instant or Instant Pages, a completely loaded page is swapped into the current tab. In that case, an `onTabReplaced` event is fired.

### Relation to webRequest events

There is no defined ordering between events of the `webRequest` API and the events of the `webNavigation` API. It is possible that `webRequest` events are still received for frames that already started a new navigation, or that a navigation only proceeds after the network resources are already fully loaded.

In general, the `webNavigation` events are closely related to the navigation state that is displayed in the UI, while the `webRequest` events correspond to the state of the network stack which is generally opaque to the user.

### Tab IDs

Not all navigating tabs correspond to actual tabs in Chrome's UI, for example, a tab that is being pre-rendered. Such tabs are not accessible using the `tabs` API nor can you request information about them by calling `webNavigation.getFrame()` or `webNavigation.getAllFrames()`. Once such a tab is swapped in, an `onTabReplaced` event is fired and they become accessible through these APIs.

### Timestamps

It's important to note that some technical oddities in the OS's handling of distinct Chrome processes can cause the clock to be skewed between the browser itself and extension processes. That means that the `timeStamp` property of the `WebNavigation` event `timeStamp` property is only guaranteed to be internally consistent. Comparing one event to another event will give you the correct offset between them, but comparing them to the current time inside the extension (using `(new Date()).getTime()`, for instance) might give unexpected results.

### Frame IDs

Frames within a tab can be identified by a frame ID. The frame ID of the main frame is always 0, the ID of child frames is a positive number. Once a document is constructed in a frame, its frame ID remains constant during the lifetime of the document. As of Chrome 49, this ID is also constant for the lifetime of the frame (across multiple navigations).

Due to the multi-process nature of Chrome, a tab might use different processes to render the source and destination of a web page. Therefore, if a navigation takes place in a new process, you might receive events both from the new and the old page until the new navigation is committed (i.e. the `onCommitted` event is sent for the new main frame). In other words, it is possible to have more than one pending sequence of `webNavigation` events with the same `frameId`. The sequences can be distinguished by the `processId` key.

Also note that during a provisional load the process might be switched several times. This happens when the load is redirected to a different site. In this case, you will receive repeated `onBeforeNavigate` and `onErrorOccurred` events, until you receive the final `onCommitted` event.

Another concept that is problematic with extensions is the lifecycle of the frame. A frame hosts a document (which is associated with a committed URL). The document can change (say by navigating) but the `frameId` won't, and so it is difficult to associate that something happened in a specific document with just `frameIds`. We are introducing a concept of a `documentId` which is a unique identifier per document. If a frame is navigated and opens a new document the identifier will change. This field is useful for determining when pages change their lifecycle state (between prerender/active/cached) because it remains the same.

### Transition types and qualifiers

The `webNavigation` `onCommitted` event has a `transitionType` and a `transitionQualifiers` property. The transition type is the same as used in the `history` API describing how the browser navigated to this particular URL. In addition, several transition qualifiers can be returned that further define the navigation.

The following transition qualifiers exist:

| Transition qualifier | Description |
| --- | --- |
| "`client_redirect`" | One or more redirects caused by JavaScript or meta refresh tags on the page happened during the navigation. |
| "`server_redirect`" | One or more redirects caused by HTTP headers sent from the server happened during the navigation. |
| "`forward_back`" | The user used the Forward or Back button to initiate the navigation. |
| "`from_address_bar`" | The user initiated the navigation from the address bar (aka Omnibox). |

## Examples

To try this API, install the `webNavigation` API example from the `chrome-extension-samples` repository.

## Types

### `TransitionQualifier`

Chrome 44+

#### Enum

"`client_redirect`"

"`server_redirect`"

"`forward_back`"

"`from_address_bar`"

### `TransitionType`

Chrome 44+

Cause of the navigation. The same transition types as defined in the `history` API are used. These are the same transition types as defined in the `history` API except with "`start_page`" in place of "`auto_toplevel`" (for backwards compatibility).

#### Enum

"`link`"

"`typed`"

"`auto_bookmark`"

"`auto_subframe`"

"`manual_subframe`"

"`generated`"

"`start_page`"

"`form_submit`"

"`reload`"

"`keyword`"

"`keyword_generated`"

## Methods

### `getAllFrames()`

Promise

```js
chrome.webNavigation.getAllFrames( details: object, callback?: function, )
```

Retrieves information about all frames of a given tab.

#### Parameters

* `details`

  object

  Information about the tab to retrieve all frames from.

  + `tabId`

    number

    The ID of the tab.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (details?: object[]) => void
  ```

  + `details`

    object[] optional

    A list of frames in the given tab, null if the specified tab ID is invalid.

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `errorOccurred`

      boolean

      True if the last navigation in this frame was interrupted by an error, i.e. the `onErrorOccurred` event fired.
    - `frameId`

      number

      The ID of the frame. 0 indicates that this is the main frame; a positive value indicates the ID of a subframe.
    - `frameType`

      `FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `url`

      string

#### Returns

* `Promise<object[] | undefined>`

  Chrome 93+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getFrame()`

Promise

```js
chrome.webNavigation.getFrame( details: object, callback?: function, )
```

Retrieves information about the given frame. A frame refers to an `<iframe>` or a `<frame>` of a web page and is identified by a tab ID and a frame ID.

#### Parameters

* `details`

  object

  Information about the frame to retrieve information about.

  + `documentId`

    string optional

    Chrome 106+

    The UUID of the document. If the `frameId` and/or `tabId` are provided they will be validated to match the document found by provided document ID.
  + `frameId`

    number optional

    The ID of the frame in the given tab.
  + `processId`

    number optional

    Deprecated since Chrome 49

    Frames are now uniquely identified by their tab ID and frame ID; the process ID is no longer needed and therefore ignored.

    The ID of the process that runs the renderer for this tab.
  + `tabId`

    number optional

    The ID of the tab in which the frame is.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (details?: object) => void
  ```

  + `details`

    object optional

    Information about the requested frame, null if the specified frame ID and/or tab ID are invalid.

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `errorOccurred`

      boolean

      True if the last navigation in this frame was interrupted by an error, i.e. the `onErrorOccurred` event fired.
    - `frameType`

      `FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `url`

      string

      The URL currently associated with this frame, if the frame identified by the `frameId` existed at one point in the given tab. The fact that an URL is associated with a given `frameId` does not imply that the corresponding frame still exists.

#### Returns

* `Promise<object | undefined>`

  Chrome 93+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onBeforeNavigate`

```js
chrome.webNavigation.onBeforeNavigate.addListener( callback: function, filters?: object, )
```

Fired when a navigation is about to occur.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique for a given tab and process.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      Deprecated since Chrome 50

      The `processId` is no longer set for this event, since the process which will render the resulting document is not known until `onCommit`.

      The value of -1.
    - `tabId`

      number

      The ID of the tab in which the navigation is about to occur.
    - `timeStamp`

      number

      The time when the browser was about to start the navigation, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCommitted`

```js
chrome.webNavigation.onCommitted.addListener( callback: function, filters?: object, )
```

Fired when a navigation is committed. The document (and the resources it refers to, such as images and subframes) might still be downloading, but at least part of the document has been received from the server and the browser has decided to switch to the new document.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCompleted`

```js
chrome.webNavigation.onCompleted.addListener( callback: function, filters?: object, )
```

Fired when a document, including the resources it refers to, is completely loaded and initialized.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the document finished loading, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCreatedNavigationTarget`

```js
chrome.webNavigation.onCreatedNavigationTarget.addListener( callback: function, filters?: object, )
```

Fired when a new window, or a new tab in an existing window, is created to host a navigation.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `sourceFrameId`

      number

      The ID of the frame with `sourceTabId` in which the navigation is triggered. 0 indicates the main frame.
    - `sourceProcessId`

      number

      The ID of the process that runs the renderer for the source frame.
    - `sourceTabId`

      number

      The ID of the tab in which the navigation is triggered.
    - `tabId`

      number

      The ID of the tab in which the url is opened
    - `timeStamp`

      number

      The time when the browser was about to create a new view, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onDOMContentLoaded`

```js
chrome.webNavigation.onDOMContentLoaded.addListener( callback: function, filters?: object, )
```

Fired when the page's DOM is fully constructed, but the referenced resources may not finish loading.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the page's DOM was fully constructed, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onErrorOccurred`

```js
chrome.webNavigation.onErrorOccurred.addListener( callback: function, filters?: object, )
```

Fired when an error occurs and the navigation is aborted. This can happen if either a network error occurred, or the user aborted the navigation.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `error`

      string

      The error description.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      Deprecated since Chrome 50

      The `processId` is no longer set for this event.

      The value of -1.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the error occurred, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onHistoryStateUpdated`

```js
chrome.webNavigation.onHistoryStateUpdated.addListener( callback: function, filters?: object, )
```

Fired when the frame's history was updated to a new URL. All future events for that frame will use the updated URL.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onReferenceFragmentUpdated`

```js
chrome.webNavigation.onReferenceFragmentUpdated.addListener( callback: function, filters?: object, )
```

Fired when the reference fragment of a frame was updated. All future events for that frame will use the updated URL.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onTabReplaced`

```js
chrome.webNavigation.onTabReplaced.addListener( callback: function, )
```

Fired when the contents of the tab is replaced by a different (usually previously pre-rendered) tab.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `replacedTabId`

      number

      The ID of the tab that was replaced.
    - `tabId`

      number

      The ID of the tab that replaced the old tab.
    - `timeStamp`

      number

      The time when the replacement happened, in milliseconds since the epoch. 

===

---
title: chrome.webRequest
url: https://developer.chrome.com/docs/extensions/reference/api/webRequest
---

Note: As of Manifest V3, the `"webRequestBlocking"` permission is no longer available for most extensions. Consider `"declarativeNetRequest"`, which enables use the `declarativeNetRequest` API. Aside from `"webRequestBlocking"`, the `webRequest` API is unchanged and available for normal use. Policy installed extensions can continue to use `"webRequestBlocking"`.

## Description

Use the `chrome.webRequest` API to observe and analyze traffic and to intercept, block, or modify requests in-flight.

## Permissions

`webRequest`

You must declare the `"webRequest"` permission in the extension manifest to use the web request API, along with the necessary host permissions. To intercept a sub-resource request, the extension must have access to both the requested URL and its initiator. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "webRequest"
  ],
  "host_permissions": [
    "*://*.google.com/*"
  ],
  ...
}
```

`webRequestBlocking`

Required to register blocking event handlers. As of Manifest V3, this is only available to policy installed extensions.

`webRequestAuthProvider`

Required to use the `onAuthRequired` method. See [Handling authentication](#handling-authentication).

## Concepts and usage

### Life cycle of requests

The web request API defines a set of events that follow the life cycle of a web request. You can use these events to observe and analyze traffic. Certain synchronous events will allow you to intercept, block, or modify a request.

The event life cycle for successful requests is illustrated here, followed by event definitions:

`onBeforeRequest` (optionally synchronous)
:   Fires when a request is about to occur. This event is sent before any TCP connection is made and can be used to cancel or redirect requests.

`onBeforeSendHeaders` (optionally synchronous)
:   Fires when a request is about to occur and the initial headers have been prepared. The event is intended to allow extensions to add, modify, and delete request headers (\*). The `onBeforeSendHeaders` event is passed to all subscribers, so different subscribers may attempt to modify the request; see the [Implementation details](#implementation-details) section for how this is handled. This event can be used to cancel the request.

`onSendHeaders`
:   Fires after all extensions have had a chance to modify the request headers, and presents the final (\*) version. The event is triggered before the headers are sent to the network. This event is informational and handled asynchronously. It does not allow modifying or cancelling the request.

`onHeadersReceived` (optionally synchronous)
:   Fires each time that an HTTP(S) response header is received. Due to redirects and authentication requests this can happen multiple times per request. This event is intended to allow extensions to add, modify, and delete response headers, such as incoming `Content-Type` headers. The caching directives are processed before this event is triggered, so modifying headers such as `Cache-Control` has no influence on the browser's cache. It also allows you to cancel or redirect the request.

`onAuthRequired` (optionally synchronous)
:   Fires when a request requires authentication of the user. This event can be handled synchronously to provide authentication credentials. Note that extensions may provide invalid credentials. Take care not to enter an infinite loop by repeatedly providing invalid credentials. This can also be used to cancel the request.

`onBeforeRedirect`
:   Fires when a redirect is about to be executed. A redirection can be triggered by an HTTP response code or by an extension. This event is informational and handled asynchronously. It does not allow you to modify or cancel the request.

`onResponseStarted`
:   Fires when the first byte of the response body is received. For HTTP requests, this means that the status line and response headers are available. This event is informational and handled asynchronously. It does not allow modifying or canceling the request.

`onCompleted`
:   Fires when a request has been processed successfully.

`onErrorOccurred`
:   Fires when a request could not be processed successfully.

The web request API guarantees that for each request, either `onCompleted` or `onErrorOccurred` is fired as the final event with one exception: If a request is redirected to a `data://` URL, `onBeforeRedirect` is the last reported event.

\* Note that the web request API presents an abstraction of the network stack to the extension. Internally, one URL request can be split into several HTTP requests (for example, to fetch individual byte ranges from a large file) or can be handled by the network stack without communicating with the network. For this reason, the API does not provide the final HTTP headers that are sent to the network. For example, all headers that are related to caching are invisible to the extension.

The following headers are currently not provided to the `onBeforeSendHeaders` event. This list is not guaranteed to be complete or stable.

*   `Authorization`
*   `Cache-Control`
*   `Connection`
*   `Content-Length`
*   `Host`
*   `If-Modified-Since`
*   `If-None-Match`
*   `If-Range`
*   `Partial-Data`
*   `Pragma`
*   `Proxy-Authorization`
*   `Proxy-Connection`
*   `Transfer-Encoding`

Starting from Chrome 79, request header modifications affect Cross-Origin Resource Sharing (CORS) checks. If modified headers for cross-origin requests do not meet the criteria, it will result in sending a CORS preflight to ask the server if such headers can be accepted. If you really need to modify headers in a way to violate the CORS protocol, you need to specify `'extraHeaders'` in `opt_extraInfoSpec`. On the other hand, response header modifications do not work to deceive CORS checks. If you need to deceive the CORS protocol, you also need to specify `'extraHeaders'` for the response modifications.

Starting from Chrome 79, the `webRequest` API does not intercept CORS preflight requests and responses by default. A CORS preflight for a request URL is visible to an extension if there is a listener with `'extraHeaders'` specified in `opt_extraInfoSpec` for the request URL. `onBeforeRequest` can also take `'extraHeaders'` from Chrome 79.

Starting from Chrome 79, the following request header is not provided and cannot be modified or removed without specifying `'extraHeaders'` in `opt_extraInfoSpec`:

*   `Origin`

Note: Modifying the `Origin` request header might not work as intended and may result in unexpected errors in the response's CORS checks. This is because while extensions can only modify the `Origin` request header, they can't change the request origin or initiator, which is a concept defined in the Fetch spec to represent who initiates the request. In such a scenario, the server may allow the CORS access for the modified request and put the header's `Origin` into the `Access-Control-Allow-Origin` header in the response. But it won't match the immutable request origin and will result in a CORS failure.

Starting from Chrome 72, if you need to modify responses before Cross Origin Read Blocking (CORB) can block the response, you need to specify `'extraHeaders'` in `opt_extraInfoSpec`.

Starting from Chrome 72, the following request headers are not provided and cannot be modified or removed without specifying `'extraHeaders'` in `opt_extraInfoSpec`:

*   `Accept-Language`
*   `Accept-Encoding`
*   `Referer`
*   `Cookie`

Starting from Chrome 72, the `Set-Cookie` response header is not provided and cannot be modified or removed without specifying `'extraHeaders'` in `opt_extraInfoSpec`.

Starting from Chrome 89, the `X-Frame-Options` response header cannot be effectively modified or removed without specifying `'extraHeaders'` in `opt_extraInfoSpec`.

Note: Specifying `'extraHeaders'` in `opt_extraInfoSpec` may have a negative impact on performance, hence it should only be used when really necessary.

The `webRequest` API only exposes requests that the extension has permission to see, given its host permissions. Moreover, only the following schemes are accessible: `http://`, `https://`, `ftp://`, `file://`, `ws://` (since Chrome 58), `wss://` (since Chrome 58), `urn:` (since Chrome 91), or `chrome-extension://`. In addition, even certain requests with URLs using one of the above schemes are hidden. These include `chrome-extension://other_extension_id` where `other_extension_id` is not the ID of the extension to handle the request, `https://www.google.com/chrome`, and other sensitive requests core to browser functionality. Also synchronous `XMLHttpRequests` from your extension are hidden from blocking event handlers in order to prevent deadlocks. Note that for some of the supported schemes the set of available events might be limited due to the nature of the corresponding protocol. For example, for the `file:` scheme, only `onBeforeRequest`, `onResponseStarted`, `onCompleted`, and `onErrorOccurred` may be dispatched.

Starting from Chrome 58, the `webRequest` API supports intercepting the WebSocket handshake request. Since the handshake is done by means of an HTTP upgrade request, its flow fits into HTTP-oriented `webRequest` model. Note that the API does not intercept:

*   Individual messages sent over an established WebSocket connection.
*   WebSocket closing connection.

Redirects are not supported for WebSocket requests.

Starting from Chrome 72, an extension will be able to intercept a request only if it has host permissions to both the requested URL and the request initiator.

Starting from Chrome 96, the `webRequest` API supports intercepting the WebTransport over HTTP/3 handshake request. Since the handshake is done by means of an HTTP CONNECT request, its flow fits into HTTP-oriented `webRequest` model. Note that:

*   Once the session is established, extensions cannot observe or intervene in the session via the `webRequest` API.
*   Modifying HTTP request headers in `onBeforeSendHeaders` is ignored.
*   Redirects and authentications are not supported in WebTransport over HTTP/3.

### Request IDs

Each request is identified by a request ID. This ID is unique within a browser session and the context of an extension. It remains constant during the life cycle of a request and can be used to match events for the same request. Note that several HTTP requests are mapped to one web request in case of HTTP redirection or HTTP authentication.

### Registering event listeners

To register an event listener for a web request, you use a variation on the usual `addListener()` function. In addition to specifying a callback function, you have to specify a filter argument, and you may specify an optional extra info argument.

The three arguments to the web request API's `addListener()` have the following definitions:

```javascript
var callback = function(details) {...};
var filter = {...};
var opt_extraInfoSpec = [...];
```

Here's an example of listening for the `onBeforeRequest` event:

```javascript
chrome.webRequest.onBeforeRequest.addListener(
    callback,
    filter,
    opt_extraInfoSpec
);
```

Each `addListener()` call takes a mandatory callback function as the first parameter. This callback function is passed a dictionary containing information about the current URL request. The information in this dictionary depends on the specific event type as well as the content of `opt_extraInfoSpec`.

If the optional `opt_extraInfoSpec` array contains the string `'blocking'` (only allowed for specific events), the callback function is handled synchronously. That means that the request is blocked until the callback function returns. In this case, the callback can return a `webRequest.BlockingResponse` that determines the further life cycle of the request. Depending on the context, this response allows canceling or redirecting a request (`onBeforeRequest`), canceling a request or modifying headers (`onBeforeSendHeaders`, `onHeadersReceived`), and canceling a request or providing authentication credentials (`onAuthRequired`).

If the optional `opt_extraInfoSpec` array contains the string `'asyncBlocking'` instead (only allowed for `onAuthRequired`), the extension can generate the `webRequest.BlockingResponse` asynchronously.

The `webRequest.RequestFilter` filter allows limiting the requests for which events are triggered in various dimensions:

`URLs`
:   URL patterns such as `*://www.google.com/foo*bar`.

`Types`
:   Request types such as `main_frame` (a document that is loaded for a top-level frame), `sub_frame` (a document that is loaded for an embedded frame), and `image` (an image on a web site). See `webRequest.RequestFilter`.

`Tab ID`
:   The identifier for one tab.

`Window ID`
:   The identifier for a window.

Depending on the event type, you can specify strings in `opt_extraInfoSpec` to ask for additional information about the request. This is used to provide detailed information on request's data only if explicitly requested.

### Handling authentication

To handle requests for HTTP authentication, add the `"webRequestAuthProvider"` permission to your manifest file:

```json
{
  "permissions": [
    "webRequest",
    "webRequestAuthProvider"
  ]
}
```

Note that this permission is not required for a policy installed extension with the `"webRequestBlocking"` permission.

To provide credentials synchronously:

```javascript
chrome.webRequest.onAuthRequired.addListener(
    (details) => {
        return { authCredentials: { username: 'guest', password: 'guest' } };
    },
    { urls: ['https://httpbin.org/basic-auth/guest/guest'] },
    ['blocking']
);
```

To provide credentials asynchronously:

```javascript
chrome.webRequest.onAuthRequired.addListener(
    (details, callback) => {
        callback({ authCredentials: { username: 'guest', password: 'guest' } });
    },
    { urls: ['https://httpbin.org/basic-auth/guest/guest'] },
    ['asyncBlocking']
);
```

### Implementation details

Several implementation details can be important to understand when developing an extension that uses the web request API:

#### web_accessible_resources

When an extension uses `webRequest` APIs to redirect a public resource request to a resource that is not web accessible, it is blocked and will result in an error. The above holds true even if the resource that is not web accessible is owned by the redirecting extension. To declare resources for use with `declarativeWebRequest` APIs, the `"web_accessible_resources"` array must be declared and populated in the manifest as documented [here](https://developer.chrome.com/docs/extensions/mv3/manifest/web_accessible_resources/).

#### Conflict resolution

In the current implementation of the web request API, a request is considered canceled if at least one extension instructs to cancel the request. If an extension cancels a request, all extensions are notified by an `onErrorOccurred` event. Only one extension can redirect a request or modify a header at a time. If more than one extension attempts to modify the request, the most recently installed extension wins, and all others are ignored. An extension is not notified if its instruction to modify or redirect has been ignored.

#### Caching

Chrome employs two caches鈥攁n on-disk cache and a very fast in-memory cache. The lifetime of an in-memory cache is attached to the lifetime of a render process, which roughly corresponds to a tab. Requests that are answered from the in-memory cache are invisible to the web request API. If a request handler changes its behavior (for example, the behavior according to which requests are blocked), a simple page refresh might not respect this changed behavior. To ensure the behavior change goes through, call `handlerBehaviorChanged()` to flush the in-memory cache. But don't do it often; flushing the cache is a very expensive operation. You don't need to call `handlerBehaviorChanged()` after registering or unregistering an event listener.

#### Timestamps

The `timestamp` property of web request events is only guaranteed to be internally consistent. Comparing one event to another event will give you the correct offset between them, but comparing them to the current time inside the extension (via `(new Date()).getTime()`, for instance) might give unexpected results.

#### Error handling

If you try to register an event with invalid arguments, then a JavaScript error will be thrown, and the event handler will not be registered. If an error is thrown while an event is handled or if an event handler returns an invalid blocking response, an error message is logged to your extension's console, and the handler is ignored for that request.

## Examples

The following example illustrates how to block all requests to `www.evil.com`:

```javascript
chrome.webRequest.onBeforeRequest.addListener(
    function(details) {
        return {cancel: details.url.indexOf("://www.evil.com/") != -1};
    },
    {urls: ["<all_urls>"]},
    ["blocking"]
);
```

As this function uses a blocking event handler, it requires the `"webRequest"` as well as the `"webRequestBlocking"` permission in the manifest file.

The following example achieves the same goal in a more efficient way because requests that are not targeted to `www.evil.com` do not need to be passed to the extension:

```javascript
chrome.webRequest.onBeforeRequest.addListener(
    function(details) { return {cancel: true}; },
    {urls: ["*://www.evil.com/*"]},
    ["blocking"]
);
```

The following example illustrates how to delete the `User-Agent` header from all requests:

```javascript
chrome.webRequest.onBeforeSendHeaders.addListener(
    function(details) {
        for (var i = 0; i < details.requestHeaders.length; ++i) {
            if (details.requestHeaders[i].name === 'User-Agent') {
                details.requestHeaders.splice(i, 1);
                break;
            }
        }
        return {requestHeaders: details.requestHeaders};
    },
    {urls: ["<all_urls>"]},
    ["blocking", "requestHeaders"]
);
```

To try the `chrome.webRequest` API, install the webRequest sample from the [chrome-extension-samples](https://github.com/GoogleChrome/chrome-extensions-samples/tree/main/api/webRequest) repository.

## Types

### BlockingResponse

Returns value for event handlers that have the `'blocking'` `extraInfoSpec` applied. Allows the event handler to modify network requests.

#### Properties

*   `authCredentials`
    *   `object` optional
    *   Only used as a response to the `onAuthRequired` event. If set, the request is made using the supplied credentials.
    *   `password`
        *   `string`
    *   `username`
        *   `string`
*   `cancel`
    *   `boolean` optional
    *   If `true`, the request is cancelled. This prevents the request from being sent. This can be used as a response to the `onBeforeRequest`, `onBeforeSendHeaders`, `onHeadersReceived` and `onAuthRequired` events.
*   `redirectUrl`
    *   `string` optional
    *   Only used as a response to the `onBeforeRequest` and `onHeadersReceived` events. If set, the original request is prevented from being sent/completed and is instead redirected to the given URL. Redirections to non-HTTP schemes such as `data:` are allowed. Redirects initiated by a redirect action use the original request method for the redirect, with one exception: If the redirect is initiated at the `onHeadersReceived` stage, then the redirect will be issued using the `GET` method. Redirects from URLs with `ws://` and `wss://` schemes are ignored.
*   `requestHeaders`
    *   `HttpHeaders` optional
    *   Only used as a response to the `onBeforeSendHeaders` event. If set, the request is made with these request headers instead.
*   `responseHeaders`
    *   `HttpHeaders` optional
    *   Only used as a response to the `onHeadersReceived` event. If set, the server is assumed to have responded with these response headers instead. Only return `responseHeaders` if you really want to modify the headers in order to limit the number of conflicts (only one extension may modify `responseHeaders` for each request).

### FormDataItem

Chrome 66+

Contains data passed within form data. For urlencoded form it is stored as string if data is utf-8 string and as `ArrayBuffer` otherwise. For `form-data` it is `ArrayBuffer`. If `form-data` represents uploading file, it is string with filename, if the filename is provided.

#### Enum

`ArrayBuffer`

`string`

### HttpHeaders

An array of HTTP headers. Each header is represented as a dictionary containing the keys `name` and either `value` or `binaryValue`.

#### Type

`object[]`

#### Properties

*   `binaryValue`
    *   `number[]` optional
    *   Value of the HTTP header if it cannot be represented by UTF-8, stored as individual byte values (0..255).
*   `name`
    *   `string`
    *   Name of the HTTP header.
*   `value`
    *   `string` optional
    *   Value of the HTTP header if it can be represented by UTF-8.

### IgnoredActionType

Chrome 70+

#### Enum

`"redirect"`

`"request_headers"`

`"response_headers"`

`"auth_credentials"`

### OnAuthRequiredOptions

Chrome 44+

#### Enum

`"responseHeaders"`: Specifies that the response headers should be included in the event.

`"blocking"`: Specifies the request is blocked until the callback function returns.

`"asyncBlocking"`: Specifies that the callback function is handled asynchronously.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnBeforeRedirectOptions

Chrome 44+

#### Enum

`"responseHeaders"`: Specifies that the response headers should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnBeforeRequestOptions

Chrome 44+

#### Enum

`"blocking"`: Specifies the request is blocked until the callback function returns.

`"requestBody"`: Specifies that the request body should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnBeforeSendHeadersOptions

Chrome 44+

#### Enum

`"requestHeaders"`: Specifies that the request header should be included in the event.

`"blocking"`: Specifies the request is blocked until the callback function returns.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnCompletedOptions

Chrome 44+

#### Enum

`"responseHeaders"`: Specifies that the response headers should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnErrorOccurredOptions

Chrome 79+

#### Value

`"extraHeaders"`

### OnHeadersReceivedOptions

Chrome 44+

#### Enum

`"blocking"`: Specifies the request is blocked until the callback function returns.

`"responseHeaders"`: Specifies that the response headers should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnResponseStartedOptions

Chrome 44+

#### Enum

`"responseHeaders"`: Specifies that the response headers should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### OnSendHeadersOptions

Chrome 44+

#### Enum

`"requestHeaders"`: Specifies that the request header should be included in the event.

`"extraHeaders"`: Specifies that headers can violate Cross-Origin Resource Sharing (CORS).

### RequestFilter

An object describing filters to apply to `webRequest` events.

#### Properties

*   `tabId`
    *   `number` optional
*   `types`
    *   `ResourceType[]` optional
    *   A list of request types. Requests that cannot match any of the types will be filtered out.
*   `urls`
    *   `string[]`
    *   A list of URLs or URL patterns. Requests that cannot match any of the URLs will be filtered out.
*   `windowId`
    *   `number` optional

### ResourceType

Chrome 44+

#### Enum

`"main_frame"`: Specifies the resource as the main frame.

`"sub_frame"`: Specifies the resource as a sub frame.

`"stylesheet"`: Specifies the resource as a stylesheet.

`"script"`: Specifies the resource as a script.

`"image"`: Specifies the resource as an image.

`"font"`: Specifies the resource as a font.

`"object"`: Specifies the resource as an object.

`"xmlhttprequest"`: Specifies the resource as an `XMLHttpRequest`.

`"ping"`: Specifies the resource as a ping.

`"csp_report"`: Specifies the resource as a Content Security Policy (CSP) report.

`"media"`: Specifies the resource as a media object.

`"websocket"`: Specifies the resource as a WebSocket.

`"webbundle"`: Specifies the resource as a WebBundle.

`"other"`: Specifies the resource as a type not included in the listed types.

### UploadData

Contains data uploaded in a URL request.

#### Properties

*   `bytes`
    *   `any` optional
    *   An `ArrayBuffer` with a copy of the data.
*   `file`
    *   `string` optional
    *   A string with the file's path and name.

## Properties

### MAX_HANDLER_BEHAVIOR_CHANGED_CALLS_PER_10_MINUTES

The maximum number of times that `handlerBehaviorChanged` can be called per 10 minute sustained interval. `handlerBehaviorChanged` is an expensive function call that shouldn't be called often.

#### Value

`20`

## Methods

### handlerBehaviorChanged()

`Promise`

```javascript
chrome.webRequest.handlerBehaviorChanged(
  callback?: function,
)
```

Needs to be called when the behavior of the `webRequest` handlers has changed to prevent incorrect handling due to caching. This function call is expensive. Don't call it often.

#### Parameters

*   `callback`
    *   `function` optional
    *   The callback parameter looks like:
        ```javascript
        () => void
        ```

#### Returns

*   `Promise<void>`
    *   Chrome 116+
    *   Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onActionIgnored

Chrome 70+

```javascript
chrome.webRequest.onActionIgnored.addListener(
  callback: function,
)
```

Fired when an extension's proposed modification to a network request is ignored. This happens in case of conflicts with other extensions.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `action`
            *   `IgnoredActionType`
            *   The proposed action which was ignored.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.

### onAuthRequired

```javascript
chrome.webRequest.onAuthRequired.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnAuthRequiredOptions[],
)
```

Fired when an authentication failure is received. The listener has three options: it can provide authentication credentials, it can cancel the request and display the error page, or it can take no action on the challenge. If bad user credentials are provided, this may be called multiple times for the same request. Note, only one of `'blocking'` or `'asyncBlocking'` modes must be specified in the `extraInfoSpec` parameter.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object, asyncCallback?: function) => BlockingResponse | undefined
        ```
    *   `details`
        *   `object`
        *   `challenger`
            *   `object`
            *   The server requesting authentication.
            *   `host`
                *   `string`
            *   `port`
                *   `number`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `isProxy`
            *   `boolean`
            *   True for `Proxy-Authenticate`, false for `WWW-Authenticate`.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `realm`
            *   `string` optional
            *   The authentication realm provided by the server, if there is one.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `responseHeaders`
            *   `HttpHeaders` optional
            *   The HTTP response headers that were received along with this response.
        *   `scheme`
            *   `string`
            *   The authentication scheme, e.g. `Basic` or `Digest`.
        *   `statusCode`
            *   `number`
            *   Chrome 43+
            *   Standard HTTP status code returned by the server.
        *   `statusLine`
            *   `string`
            *   HTTP status line of the response or the `'HTTP/0.9 200 OK'` string for HTTP/0.9 responses (i.e., responses that lack a status line) or an empty string if there are no headers.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
    *   `asyncCallback`
        *   `function` optional
        *   Chrome 58+
        *   The `asyncCallback` parameter looks like:
            ```javascript
            (response: BlockingResponse) => void
            ```
        *   `response`
            *   `BlockingResponse`
    *   `returns`
        *   `BlockingResponse | undefined`
        *   If `"blocking"` is specified in the `"extraInfoSpec"` parameter, the event listener should return an object of this type.
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnAuthRequiredOptions[]` optional

### onBeforeRedirect

```javascript
chrome.webRequest.onBeforeRedirect.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnBeforeRedirectOptions[],
)
```

Fired when a server-initiated redirect is about to occur.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `fromCache`
            *   `boolean`
            *   Indicates if this response was fetched from disk cache.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `ip`
            *   `string` optional
            *   The server IP address that the request was actually sent to. Note that it may be a literal IPv6 address.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `redirectUrl`
            *   `string`
            *   The new URL.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `responseHeaders`
            *   `HttpHeaders` optional
            *   The HTTP response headers that were received along with this redirect.
        *   `statusCode`
            *   `number`
            *   Standard HTTP status code returned by the server.
        *   `statusLine`
            *   `string`
            *   HTTP status line of the response or the `'HTTP/0.9 200 OK'` string for HTTP/0.9 responses (i.e., responses that lack a status line) or an empty string if there are no headers.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnBeforeRedirectOptions[]` optional

### onBeforeRequest

```javascript
chrome.webRequest.onBeforeRequest.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnBeforeRequestOptions[],
)
```

Fired when a request is about to occur.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => BlockingResponse | undefined
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle` optional
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType` optional
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestBody`
            *   `object` optional
            *   Contains the HTTP request body data. Only provided if `extraInfoSpec` contains `'requestBody'`.
            *   `error`
                *   `string` optional
                *   Errors when obtaining request body data.
            *   `formData`
                *   `object` optional
                *   If the request method is `POST` and the body is a sequence of key-value pairs encoded in UTF8, encoded as either `multipart/form-data`, or `application/x-www-form-urlencoded`, this dictionary is present and for each key contains the list of all values for that key. If the data is of another media type, or if it is malformed, the dictionary is not present. An example value of this dictionary is `{'key': ['value1', 'value2']}`.
            *   `raw`
                *   `UploadData[]` optional
                *   If the request method is `PUT` or `POST`, and the body is not already parsed in `formData`, then the unparsed request body elements are contained in this array.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
    *   `returns`
        *   `BlockingResponse | undefined`
        *   If `"blocking"` is specified in the `"extraInfoSpec"` parameter, the event listener should return an object of this type.
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnBeforeRequestOptions[]` optional

### onBeforeSendHeaders

```javascript
chrome.webRequest.onBeforeSendHeaders.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnBeforeSendHeadersOptions[],
)
```

Fired before sending an HTTP request, once the request headers are available. This may occur after a TCP connection is made to the server, but before any HTTP data is sent.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => BlockingResponse | undefined
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestHeaders`
            *   `HttpHeaders` optional
            *   The HTTP request headers that are going to be sent out with this request.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
    *   `returns`
        *   `BlockingResponse | undefined`
        *   If `"blocking"` is specified in the `"extraInfoSpec"` parameter, the event listener should return an object of this type.
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnBeforeSendHeadersOptions[]` optional

### onCompleted

```javascript
chrome.webRequest.onCompleted.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnCompletedOptions[],
)
```

Fired when a request is completed.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `fromCache`
            *   `boolean`
            *   Indicates if this response was fetched from disk cache.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `ip`
            *   `string` optional
            *   The server IP address that the request was actually sent to. Note that it may be a literal IPv6 address.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `responseHeaders`
            *   `HttpHeaders` optional
            *   The HTTP response headers that were received along with this response.
        *   `statusCode`
            *   `number`
            *   Standard HTTP status code returned by the server.
        *   `statusLine`
            *   `string`
            *   HTTP status line of the response or the `'HTTP/0.9 200 OK'` string for HTTP/0.9 responses (i.e., responses that lack a status line) or an empty string if there are no headers.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnCompletedOptions[]` optional

### onErrorOccurred

```javascript
chrome.webRequest.onErrorOccurred.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnErrorOccurredOptions[],
)
```

Fired when an error occurs.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request. This value is not present if the request is a navigation of a frame.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `error`
            *   `string`
            *   The error description. This string is not guaranteed to remain backwards compatible between releases. You must not parse and act based upon its content.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `fromCache`
            *   `boolean`
            *   Indicates if this response was fetched from disk cache.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `ip`
            *   `string` optional
            *   The server IP address that the request was actually sent to. Note that it may be a literal IPv6 address.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnErrorOccurredOptions[]` optional

### onHeadersReceived

```javascript
chrome.webRequest.onHeadersReceived.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnHeadersReceivedOptions[],
)
```

Fired when HTTP response headers of a request have been received.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => BlockingResponse | undefined
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `responseHeaders`
            *   `HttpHeaders` optional
            *   The HTTP response headers that have been received with this response.
        *   `statusCode`
            *   `number`
            *   Chrome 43+
            *   Standard HTTP status code returned by the server.
        *   `statusLine`
            *   `string`
            *   HTTP status line of the response or the `'HTTP/0.9 200 OK'` string for HTTP/0.9 responses (i.e., responses that lack a status line).
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
    *   `returns`
        *   `BlockingResponse | undefined`
        *   If `"blocking"` is specified in the `"extraInfoSpec"` parameter, the event listener should return an object of this type.
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnHeadersReceivedOptions[]` optional

### onResponseStarted

```javascript
chrome.webRequest.onResponseStarted.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnResponseStartedOptions[],
)
```

Fired when the first byte of the response body is received. For HTTP requests, this means that the status line and response headers are available.

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `fromCache`
            *   `boolean`
            *   Indicates if this response was fetched from disk cache.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `ip`
            *   `string` optional
            *   The server IP address that the request was actually sent to. Note that it may be a literal IPv6 address.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `responseHeaders`
            *   `HttpHeaders` optional
            *   The HTTP response headers that were received along with this response.
        *   `statusCode`
            *   `number`
            *   Standard HTTP status code returned by the server.
        *   `statusLine`
            *   `string`
            *   HTTP status line of the response or the `'HTTP/0.9 200 OK'` string for HTTP/0.9 responses (i.e., responses that lack a status line) or an empty string if there are no headers.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnResponseStartedOptions[]` optional

### onSendHeaders

```javascript
chrome.webRequest.onSendHeaders.addListener(
  callback: function,
  filter: RequestFilter,
  extraInfoSpec?: OnSendHeadersOptions[],
)
```

Fired just before a request is going to be sent to the server (modifications of previous `onBeforeSendHeaders` callbacks are visible by the time `onSendHeaders` is fired).

#### Parameters

*   `callback`
    *   `function`
    *   The callback parameter looks like:
        ```javascript
        (details: object) => void
        ```
    *   `details`
        *   `object`
        *   `documentId`
            *   `string`
            *   Chrome 106+
            *   The UUID of the document making the request.
        *   `documentLifecycle`
            *   `extensionTypes.DocumentLifecycle`
            *   Chrome 106+
            *   The lifecycle the document is in.
        *   `frameId`
            *   `number`
            *   The value `0` indicates that the request happens in the main frame; a positive value indicates the ID of a subframe in which the request happens. If the document of a (sub-)frame is loaded (type is `main_frame` or `sub_frame`), `frameId` indicates the ID of this frame, not the ID of the outer frame. Frame IDs are unique within a tab.
        *   `frameType`
            *   `extensionTypes.FrameType`
            *   Chrome 106+
            *   The type of frame the request occurred in.
        *   `initiator`
            *   `string` optional
            *   Chrome 63+
            *   The origin where the request was initiated. This does not change through redirects. If this is an opaque origin, the string `'null'` will be used.
        *   `method`
            *   `string`
            *   Standard HTTP method.
        *   `parentDocumentId`
            *   `string` optional
            *   Chrome 106+
            *   The UUID of the parent document owning this frame. This is not set if there is no parent.
        *   `parentFrameId`
            *   `number`
            *   ID of frame that wraps the frame which sent the request. Set to `-1` if no parent frame exists.
        *   `requestHeaders`
            *   `HttpHeaders` optional
            *   The HTTP request headers that have been sent out with this request.
        *   `requestId`
            *   `string`
            *   The ID of the request. Request IDs are unique within a browser session. As a result, they could be used to relate different events of the same request.
        *   `tabId`
            *   `number`
            *   The ID of the tab in which the request takes place. Set to `-1` if the request isn't related to a tab.
        *   `timeStamp`
            *   `number`
            *   The time when this signal is triggered, in milliseconds since the epoch.
        *   `type`
            *   `ResourceType`
            *   How the requested resource will be used.
        *   `url`
            *   `string`
*   `filter`
    *   `RequestFilter`
*   `extraInfoSpec`
    *   `OnSendHeadersOptions[]` optional 

===

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

Gets the window that was most recently focused 鈥?typically the window 'on top'.

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
</chrome-api>
