# DevTools

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/devtools
- **Version**: All versions

## Overview
Enables extensions to interact with the browser's Developer Tools. You use this API to create Developer Tools pages, interact with the window that is being inspected, and inspect the page network usage.

This API provides three main namespaces: inspectedWindow for interacting with the inspected window, network for monitoring network activity, and panels for creating custom DevTools panels.

## Permissions
- Manifest key: `devtools_page` - required to use the API
- Optional permission: `devtools` - to avoid install-time warning (Firefox only)

## Namespaces

### devtools.inspectedWindow
Interact with the window that Developer tools are attached to.

#### Properties
- `tabId` - The ID of the tab being inspected

#### Methods
- `eval()` - Evaluates JavaScript in the inspected window
- `reload()` - Reloads the inspected window
- `getResources()` - Gets all resources in the inspected page

#### Events
- `onResourceAdded` - Fired when a new resource is added
- `onResourceContentCommitted` - Fired when resource content is committed

### devtools.network
Obtain information about network requests associated with the inspected window.

#### Methods
- `getHAR()` - Gets the HAR log for the inspected window

#### Events
- `onRequestFinished` - Fired when a network request is finished
- `onNavigated` - Fired when the inspected window navigates to a new page

### devtools.panels
Create User Interface panels that will be displayed inside Developer Tools.

#### Properties
- `elements` - A reference to the Elements panel
- `sources` - A reference to the Sources panel
- `themeName` - The name of the current DevTools theme

#### Methods
- `create()` - Creates a new DevTools panel
- `setOpenResourceHandler()` - Sets a handler for resource links
- `openResource()` - Opens a resource in the DevTools

#### Types
##### ExtensionPanel
Represents a DevTools panel created by the extension.

##### ExtensionSidebarPane
Represents a sidebar pane within a DevTools panel.

## Manifest Configuration
```json
{
  "devtools_page": "devtools/devtools.html",
  "optional_permissions": ["devtools"]
}
```

## Code Examples
In devtools.html:
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <script src="devtools.js"></script>
  </body>
</html>
```

In devtools.js:
```javascript
// Create a new panel
browser.devtools.panels.create(
  "My Panel",      // title
  "icon.png",      // icon
  "panel.html"     // content
).then((newPanel) => {
  // Panel created
});

// Listen for network requests
browser.devtools.network.onRequestFinished.addListener((request) => {
  console.log("Request completed:", request.request.url);
});

// Evaluate code in the inspected window
browser.devtools.inspectedWindow.eval(
  "document.body.style.backgroundColor = 'red'"
);
```

## Related APIs
- `tabs` - For general tab manipulation
- `webRequest` - For intercepting network requests
- `debugger` - For debugging JavaScript