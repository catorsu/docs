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