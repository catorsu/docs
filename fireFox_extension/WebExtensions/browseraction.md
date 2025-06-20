# BrowserAction

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browserAction
- **Version**: Manifest V2 (deprecated in favor of action API in Manifest V3)

## Overview
Read and modify attributes of and listen to clicks on the browser toolbar button defined with the browser_action manifest key. A browser action is a button in the browser's toolbar.

You can associate a popup with the button. Like a web page, the popup is specified using HTML, CSS, and JavaScript. JavaScript running in the popup gets access to the same WebExtension APIs as your background scripts, but its global context is the popup, not the current page displayed in the browser.

## Permissions
- No special permissions required

## Types
### ColorArray
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| R | integer | Yes | - | Red component (0-255) |
| G | integer | Yes | - | Green component (0-255) |
| B | integer | Yes | - | Blue component (0-255) |
| A | integer | Yes | - | Alpha component (0-255) |

### ImageDataType
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| data | ImageData | Yes | - | Pixel data for an image. Must be an ImageData object (for example, from a canvas element) |

## Methods
### setTitle()
**Syntax**: `browser.browserAction.setTitle(details)`

Sets the browser action's title. This will be displayed in a tooltip.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing title details |
| details.title | string | Yes | - | The string the browser action should display when moused over |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled with no arguments when the title has been set

#### Code Examples
No code examples in source documentation

### getTitle()
**Syntax**: `browser.browserAction.getTitle(details)`

Gets the browser action's title.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which title to get |
| details.tabId | integer | No | - | Specify the tab to get the title from |
| details.windowId | integer | No | - | Specify the window to get the title from |

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with the title string

#### Code Examples
No code examples in source documentation

### setIcon()
**Syntax**: `browser.browserAction.setIcon(details)`

Sets the browser action's icon.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing icon details |
| details.imageData | ImageDataType or object | No | - | Either an ImageData object or a dictionary {size -> ImageData} |
| details.path | string or object | No | - | Either a relative path or a dictionary {size -> relative path} |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the icon has been set

#### Code Examples
No code examples in source documentation

### setPopup()
**Syntax**: `browser.browserAction.setPopup(details)`

Sets the HTML document to be opened as a popup when the user clicks on the browser action's icon.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing popup details |
| details.popup | string | Yes | - | The relative path to the HTML file to show in a popup. If set to empty string, no popup is shown |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the popup has been set

#### Code Examples
No code examples in source documentation

### getPopup()
**Syntax**: `browser.browserAction.getPopup(details)`

Gets the HTML document set as the browser action's popup.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which popup to get |
| details.tabId | integer | No | - | Specify the tab to get the popup from |
| details.windowId | integer | No | - | Specify the window to get the popup from |

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with the popup URL

#### Code Examples
No code examples in source documentation

### openPopup()
**Syntax**: `browser.browserAction.openPopup()`

Open the browser action's popup.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the popup is shown

#### Code Examples
No code examples in source documentation

### setBadgeText()
**Syntax**: `browser.browserAction.setBadgeText(details)`

Sets the browser action's badge text. The badge is displayed on top of the icon.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing badge text details |
| details.text | string | Yes | - | Any number of characters can be passed, but only about four can fit in the space |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the badge text has been set

#### Code Examples
No code examples in source documentation

### getBadgeText()
**Syntax**: `browser.browserAction.getBadgeText(details)`

Gets the browser action's badge text.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which badge text to get |
| details.tabId | integer | No | - | Specify the tab to get the badge text from |
| details.windowId | integer | No | - | Specify the window to get the badge text from |

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with the badge text

#### Code Examples
No code examples in source documentation

### setBadgeBackgroundColor()
**Syntax**: `browser.browserAction.setBadgeBackgroundColor(details)`

Sets the badge's background color.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing badge background color details |
| details.color | string or ColorArray | Yes | - | The color, specified as a CSS color value or a ColorArray |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the badge background color has been set

#### Code Examples
No code examples in source documentation

### getBadgeBackgroundColor()
**Syntax**: `browser.browserAction.getBadgeBackgroundColor(details)`

Gets the badge's background color.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which badge background color to get |
| details.tabId | integer | No | - | Specify the tab to get the badge background color from |
| details.windowId | integer | No | - | Specify the window to get the badge background color from |

#### Returns
- **Type**: `Promise<ColorArray>`
- **Description**: Fulfilled with the retrieved color as a ColorArray

#### Code Examples
```javascript
function onGot(color) {
  console.log(color);
}

function onFailure(error) {
  console.log(error);
}

browser.browserAction.getBadgeBackgroundColor({}).then(onGot, onFailure);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browserAction/getBadgeBackgroundColor

### setBadgeTextColor()
**Syntax**: `browser.browserAction.setBadgeTextColor(details)`

Sets the badge's text color.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing badge text color details |
| details.color | string or ColorArray | Yes | - | The color, specified as a CSS color value or a ColorArray |
| details.tabId | integer | No | - | Limits the change to when a particular tab is selected |
| details.windowId | integer | No | - | Limits the change to when a particular window is focused |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the badge text color has been set

#### Code Examples
No code examples in source documentation

### getBadgeTextColor()
**Syntax**: `browser.browserAction.getBadgeTextColor(details)`

Gets the badge's text color.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which badge text color to get |
| details.tabId | integer | No | - | Specify the tab to get the badge text color from |
| details.windowId | integer | No | - | Specify the window to get the badge text color from |

#### Returns
- **Type**: `Promise<ColorArray>`
- **Description**: Fulfilled with the retrieved color as a ColorArray

#### Code Examples
```javascript
function onGot(color) {
  console.log(color);
}

function onFailure(error) {
  console.log(error);
}

browser.browserAction.getBadgeTextColor({}).then(onGot, onFailure);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browserAction/getBadgeTextColor

### getUserSettings()
**Syntax**: `browser.browserAction.getUserSettings()`

Gets the user-specified settings for the browser action.

#### Parameters
None

#### Returns
- **Type**: `Promise<object>`
- **Description**: Fulfilled with an object containing the user settings

#### Code Examples
No code examples in source documentation

### enable()
**Syntax**: `browser.browserAction.enable(tabId)`

Enables the browser action for a tab. By default, browser actions are enabled for all tabs.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | No | - | The id of the tab for which to enable the browser action |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the browser action is enabled

#### Code Examples
No code examples in source documentation

### disable()
**Syntax**: `browser.browserAction.disable(tabId)`

Disables the browser action for a tab, meaning that it cannot be clicked when that tab is active.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | No | - | The id of the tab for which to disable the browser action |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the browser action is disabled

#### Code Examples
No code examples in source documentation

### isEnabled()
**Syntax**: `browser.browserAction.isEnabled(details)`

Checks whether the browser action is enabled or not.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object specifying which browser action to check |
| details.tabId | integer | No | - | Specify the tab to check |
| details.windowId | integer | No | - | Specify the window to check |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: Fulfilled with true if the browser action is enabled

#### Code Examples
No code examples in source documentation

## Events
### onClicked
**Fired when**: A browser action icon is clicked. This event will not fire if the browser action has a popup.

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| tab | tabs.Tab | The tab that was active when the icon was clicked |
| info | object | An object containing information about the click |
| info.modifiers | array | An array of keyboard modifiers that were held while the menu item was clicked |
| info.button | integer | An integer indicating which button was pressed (0 for left-click) |

## Related APIs
- `action` - Manifest V3 replacement for this API
- `pageAction` - For page-specific actions
- `menus` - For adding context menu items to the browser action button