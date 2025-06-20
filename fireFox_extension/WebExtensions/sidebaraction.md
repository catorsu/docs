# sidebarAction

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction
- **Version**: Current (as of June 2025)

## Overview

Gets and sets properties of an extension's sidebar. A sidebar is a pane displayed at the left or right of a web page, next to the web content. The browser provides a UI that enables the user to see the available sidebars and select one to display. Extensions define sidebars using the `sidebar_action` manifest.json key and can control sidebar properties using this API.

The sidebarAction API is based on Opera's sidebarAction API and closely modeled on the browserAction API. However, Firefox has not implemented `setBadgeText()`, `getBadgeText()`, `setBadgeBackgroundColor()`, `getBadgeBackgroundColor()`, `onFocus`, and `onBlur`.

## Permissions

To use this API, declare the `sidebar_action` key in your manifest.json file. No additional permissions are required for the sidebarAction API itself.

## Types

### ImageDataType
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| imageData | ImageData or object | No | - | Pixel data for an image. Must be an ImageData object (for example, from a `<canvas>` element) |

## Methods

### close()
**Syntax**: `browser.sidebarAction.close()`

Closes the sidebar in the active window, if it is the extension's own sidebar.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves with no arguments when the operation completes

#### Code Examples
```javascript
browser.menus.create({
  id: "close-sidebar",
  title: "close sidebar",
  contexts: ["all"]
});

browser.menus.onClicked.addListener(() => {
  browser.sidebarAction.close();
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/close

### getPanel()
**Syntax**: `browser.sidebarAction.getPanel(details)`

Gets a URL to the HTML document that defines the sidebar's contents.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | No | {} | Specifies which sidebar to get the panel for |
| details.tabId | integer | No | - | Get the panel for this specific tab |
| details.windowId | integer | No | - | Get the panel for this specific window |

#### Returns
- **Type**: `Promise<string>`
- **Description**: A Promise that resolves to the URL of the sidebar's panel

#### Code Examples
```javascript
function onGot(sidebarUrl) {
  console.log(sidebarUrl);
}

let gettingPanel = browser.sidebarAction.getPanel({});
gettingPanel.then(onGot);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/getPanel

### getTitle()
**Syntax**: `browser.sidebarAction.getTitle(details)`

Gets the sidebar's title.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | No | {} | Specifies which sidebar to get the title for |
| details.tabId | integer | No | - | Get the title for this specific tab |
| details.windowId | integer | No | - | Get the title for this specific window |

#### Returns
- **Type**: `Promise<string>`
- **Description**: A Promise that resolves to the sidebar's title

#### Code Examples
```javascript
function toggleTitle(title) {
  if (title == "this") {
    browser.sidebarAction.setTitle({title: "that"});
  } else {
    browser.sidebarAction.setTitle({title: "this"});
  }
}

browser.browserAction.onClicked.addListener(() => {
  let gettingTitle = browser.sidebarAction.getTitle({});
  gettingTitle.then(toggleTitle);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/getTitle

### isOpen()
**Syntax**: `browser.sidebarAction.isOpen(details)`

Checks whether the sidebar is open.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | No | {} | Specifies which window to check |
| details.windowId | integer | No | - | Check this specific window |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: A Promise that resolves to true if the sidebar is open

#### Code Examples
No code examples in source documentation

### open()
**Syntax**: `browser.sidebarAction.open()`

Open the sidebar in the active window.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the operation completes

#### Code Examples
```javascript
browser.menus.create({
  id: "open-sidebar",
  title: "open sidebar",
  contexts: ["all"]
});

browser.menus.onClicked.addListener(() => {
  browser.sidebarAction.open();
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/open

### setIcon()
**Syntax**: `browser.sidebarAction.setIcon(details)`

Sets the icon for the sidebar. You can specify a single icon as either the path to an image file or a sidebarAction.ImageDataType object. You can specify multiple icons in different sizes by supplying a dictionary containing multiple paths or ImageData objects.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Icon specification |
| details.imageData | ImageData or object | No | - | ImageData object or dictionary of ImageData objects in different sizes |
| details.path | string or object | No | - | Path to icon file or dictionary of paths for different sizes |
| details.tabId | integer | No | - | Set icon for this specific tab |
| details.windowId | integer | No | - | Set icon for this specific window |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the icon is set

#### Code Examples
```javascript
var on = false;

function toggle(tab) {
  if (on) {
    browser.sidebarAction.setIcon({
      path: "off.svg",
      tabId: tab.id
    });
    on = false;
  } else {
    browser.sidebarAction.setIcon({
      path: "on.svg", 
      tabId: tab.id
    });
    on = true;
  }
}

browser.browserAction.onClicked.addListener(toggle);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/setIcon

### setPanel()
**Syntax**: `browser.sidebarAction.setPanel(details)`

Sets the sidebar's panel: that is, the HTML document that defines the content of this sidebar.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Panel specification |
| details.panel | string | Yes | - | The path to the HTML file to load in the sidebar |
| details.tabId | integer | No | - | Set panel for this specific tab |
| details.windowId | integer | No | - | Set panel for this specific window |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the panel is set

#### Code Examples
```javascript
let thisPanel = browser.runtime.getURL("/this.html");
let thatPanel = browser.runtime.getURL("/that.html");

function toggle(panel) {
  if (panel === thisPanel) {
    browser.sidebarAction.setPanel({panel: thatPanel});
  } else {
    browser.sidebarAction.setPanel({panel: thisPanel});
  }
}

browser.browserAction.onClicked.addListener(() => {
  browser.sidebarAction.getPanel({}).then(toggle);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sidebarAction/setPanel

### setTitle()
**Syntax**: `browser.sidebarAction.setTitle(details)`

Sets the sidebar's title. This will be displayed in any UI provided by the browser to list sidebars, such as a menu.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Title specification |
| details.title | string | Yes | - | The new title for the sidebar |
| details.tabId | integer | No | - | Set title for this specific tab |
| details.windowId | integer | No | - | Set title for this specific window |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the title is set

#### Code Examples
No code examples in source documentation

### toggle()
**Syntax**: `browser.sidebarAction.toggle()`

Toggles the visibility of the sidebar.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the operation completes

#### Code Examples
No code examples in source documentation

## Events

No events are documented for this API.

## Related APIs
- `browserAction` - Similar API for browser toolbar buttons
- `pageAction` - Similar API for page-specific actions
- `sidebar_action` - Manifest key for defining sidebar properties
