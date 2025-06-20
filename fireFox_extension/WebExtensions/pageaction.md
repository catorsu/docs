# pageAction

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction
- **Version**: Current as of June 2025

## Overview

Read and modify attributes of and listen to clicks on the address bar button defined with the `page_action` manifest key. Page actions are for actions that are only relevant to particular pages (such as "bookmark the current tab"). If they are relevant to the browser as a whole (such as "show all bookmarks"), use a browser action instead.

The button also has a context menu, and you can add items to this menu with the `menus` API using the `page_action` context type.

## Permissions
- `activeTab` - recommended for most use cases

## Types

### ImageDataType
Pixel data for an image. Must be an ImageData object (for example, from a `<canvas>` element).

## Methods

### show()
**Syntax**: `browser.pageAction.show(tabId)`

Shows the page action for a given tab. The page action is shown whenever the given tab is the active tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | Yes | - | The ID of the tab for which you want to show the page action |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with undefined once the page action is shown

#### Code Examples
```javascript
browser.contextMenus.create({
  id: "show",
  title: "Show page action",
});

browser.contextMenus.onClicked.addListener((info, tab) => {
  if (info.menuItemId === "show") {
    browser.pageAction.show(tab.id);
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction/show#examples

### hide()
**Syntax**: `browser.pageAction.hide(tabId)`

Hides the page action for a given tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | Yes | - | The ID of the tab for which you want to hide the page action |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with undefined once the page action is hidden

### isShown()
**Syntax**: `browser.pageAction.isShown(details)`

Checks whether the page action is shown or not.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing tabId property |
| details.tabId | integer | Yes | - | The ID of the tab to check |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: A Promise that will be fulfilled with true if the page action is shown, false otherwise

### setTitle()
**Syntax**: `browser.pageAction.setTitle(details)`

Sets the title of the page action. The title is displayed in a tooltip when the user hovers over the page action.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing title and tabId |
| details.tabId | integer | Yes | - | The ID of the tab whose title you want to set |
| details.title | string\|null | Yes | - | The tooltip text. If null is passed, the title is reset to the title specified in the page_action manifest key |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with undefined once the title is set

#### Code Examples
```javascript
browser.tabs.onUpdated.addListener((tabId, changeInfo, tabInfo) => {
  browser.pageAction.show(tabId);
  browser.pageAction.setTitle({
    tabId,
    title: `Tab ID: ${tabId}`,
  });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction/setTitle#examples

### getTitle()
**Syntax**: `browser.pageAction.getTitle(details)`

Gets the page action's title.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing tabId property |
| details.tabId | integer | Yes | - | The ID of the tab to get the title for |

#### Returns
- **Type**: `Promise<string>`
- **Description**: A Promise that will be fulfilled with the page action's title

### setIcon()
**Syntax**: `browser.pageAction.setIcon(details)`

Sets the icon for the page action. You can specify a single icon as either a path or ImageDataType object, or multiple icons in different sizes.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing icon data and tabId |
| details.tabId | integer | Yes | - | The ID of the tab whose icon you want to set |
| details.imageData | ImageDataType\|object | No | - | Either a single ImageData object or dictionary of multiple sizes |
| details.path | string\|object | No | - | Either a relative path to an icon file or dictionary of multiple sizes |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with no arguments once the icon has been set

#### Code Examples
```javascript
browser.pageAction.onClicked.addListener((tab) => {
  browser.pageAction.setIcon({
    tabId: tab.id,
    path: "icons/icon-48.png",
  });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction/setIcon#examples

### setPopup()
**Syntax**: `browser.pageAction.setPopup(details)`

Sets the HTML document to be opened as a popup when the user clicks on the page action's icon.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing popup and tabId |
| details.tabId | integer | Yes | - | The ID of the tab whose popup you want to set |
| details.popup | string\|null | Yes | - | The relative path to the HTML file to show as popup. If null, removes the popup |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with undefined once the popup is set

#### Code Examples
```javascript
browser.tabs.onUpdated.addListener((tabId, changeInfo, tabInfo) => {
  if (changeInfo.status) {
    browser.pageAction.show(tabId);
    if (changeInfo.status === "loading") {
      browser.pageAction.setPopup({
        tabId,
        popup: "/popup/loading.html",
      });
    } else {
      browser.pageAction.setPopup({
        tabId,
        popup: "/popup/complete.html",
      });
    }
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction/setPopup#examples

### getPopup()
**Syntax**: `browser.pageAction.getPopup(details)`

Gets the URL for the page action's popup.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing tabId property |
| details.tabId | integer | Yes | - | The ID of the tab to get the popup for |

#### Returns
- **Type**: `Promise<string>`
- **Description**: A Promise that will be fulfilled with the popup's URL

### openPopup()
**Syntax**: `browser.pageAction.openPopup()`

Opens the page action's popup.

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: A Promise that will be fulfilled with undefined once the popup is opened

## Events

### onClicked
**Fired when**: A page action icon is clicked. This event will not fire if the page action has a popup.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| tab | tabs.Tab | A tabs.Tab object representing the tab whose page action was clicked |
| OnClickData | object | An object containing information about the click |
| OnClickData.modifiers | array | The keyboard modifiers active at the time of the click (Shift, Alt, Command, Ctrl, or MacCtrl) |
| OnClickData.button | integer | The button used to click: 0 for left-click, 1 for middle button |

#### Code Examples
```javascript
let catGifs = "https://giphy.com/explore/cat";

browser.pageAction.onClicked.addListener((tab) => {
  browser.pageAction.hide(tab.id);
  browser.tabs.update({ url: catGifs });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pageAction/onClicked#examples

## Related APIs
- `action` - Modern replacement for pageAction in Manifest V3
- `browserAction` - For browser-wide actions (deprecated in Manifest V3)
- `menus` - For adding context menu items to page actions
- `tabs` - For working with browser tabs
