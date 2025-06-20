# runtime

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/runtime
- **Version**: Current as of June 2025

## Overview

This module provides information about your extension and the environment it's running in. It also provides messaging APIs enabling you to communicate between different parts of your extension, with other extensions, and with native applications.

No specific permissions are required for most runtime API features.

## Permissions
- None required for most features
- `nativeMessaging` - for native application communication

## Types

### Port
Represents one end of a connection between two specific contexts for message exchange.

### MessageSender
Contains information about the sender of a message or connection request with properties:
- **tab**: tabs.Tab object (if sent from content script)
- **frameId**: number - Frame ID of sender
- **id**: string - Extension ID of sender
- **url**: string - URL of page/frame that sent message
- **tlsChannelId**: string - TLS channel ID

### PlatformInfo
Contains information about the platform the browser is running on:
- **os**: string - "mac", "win", "android", "cros", "linux", "openbsd"
- **arch**: string - "arm", "arm64", "x86-32", "x86-64", "mips", "mips64"

## Properties

### lastError
**Type**: `object | undefined`

This value is set when an asynchronous function has an error condition that it needs to report to its caller.

### id
**Type**: `string`

The ID of the extension.

## Methods

### getManifest()
**Syntax**: `browser.runtime.getManifest()`

Gets the complete manifest.json file, serialized as an object.

#### Returns
- **Type**: `object`
- **Description**: The manifest.json content as a JavaScript object

#### Code Examples
```javascript
function logManifestData() {
  console.log(browser.runtime.getManifest());
}
```

### getURL()
**Syntax**: `browser.runtime.getURL(path)`

Given a relative path from the manifest.json to a resource packaged with the extension, returns a fully-qualified URL.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| path | string | Yes | - | Relative path from manifest.json to resource |

#### Returns
- **Type**: `string`
- **Description**: Fully-qualified URL to the resource

#### Code Examples
```javascript
// Get URL for a packaged image
let imageURL = browser.runtime.getURL("images/my-image.png");
```

### sendMessage()
**Syntax**: `browser.runtime.sendMessage(extensionId, message, options)`

Sends a message to event listeners within your extension or a different extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| extensionId | string | No | - | Extension ID to send to (omit for own extension) |
| message | any | Yes | - | Message to send |
| options | object | No | - | Additional options |

#### Returns
- **Type**: `Promise<any>`
- **Description**: Promise that resolves to the response from the message listener

#### Code Examples
```javascript
// Send message within extension
browser.runtime.sendMessage({
  action: "updateIcon",
  data: "some data"
}).then(response => {
  console.log("Response:", response);
});
```

### connect()
**Syntax**: `browser.runtime.connect(extensionId, connectInfo)`

Establishes a connection from a content script to the main extension process, or from one extension to a different extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| extensionId | string | No | - | Extension ID to connect to |
| connectInfo | object | No | - | Connection configuration |
| connectInfo.name | string | No | - | Name for the connection |
| connectInfo.includeTlsChannelId | boolean | No | false | Include TLS channel ID |

#### Returns
- **Type**: `Port`
- **Description**: Port object for the connection

#### Code Examples
```javascript
let port = browser.runtime.connect({name: "my-connection"});
port.postMessage({action: "ping"});
port.onMessage.addListener((msg) => {
  console.log("Received:", msg);
});
```

### reload()
**Syntax**: `browser.runtime.reload()`

Reloads the extension.

#### Returns
- **Type**: `undefined`
- **Description**: No return value

### openOptionsPage()
**Syntax**: `browser.runtime.openOptionsPage()`

Opens your extension's options page.

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when options page is opened

### getPlatformInfo()
**Syntax**: `browser.runtime.getPlatformInfo()`

Returns information about the current platform.

#### Returns
- **Type**: `Promise<PlatformInfo>`
- **Description**: Promise that resolves to platform information

### getBrowserInfo()
**Syntax**: `browser.runtime.getBrowserInfo()`

Returns information about the browser in which this extension is installed.

#### Returns
- **Type**: `Promise<object>`
- **Description**: Promise that resolves to browser information with name, version, and buildID

### sendNativeMessage()
**Syntax**: `browser.runtime.sendNativeMessage(application, message)`

Sends a message from an extension to a native application.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| application | string | Yes | - | Name of native application |
| message | object | Yes | - | Message to send to native app |

#### Returns
- **Type**: `Promise<any>`
- **Description**: Promise that resolves to the response from the native application

### connectNative()
**Syntax**: `browser.runtime.connectNative(application)`

Connects the extension to a native application on the user's computer.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| application | string | Yes | - | Name of native application |

#### Returns
- **Type**: `Port`
- **Description**: Port object for communicating with the native application

## Events

### onStartup
**Fired when**: A profile that has this extension installed first starts up.

### onInstalled
**Fired when**: The extension is first installed, updated to a new version, or when the browser is updated.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| details | object | Installation details |
| details.reason | string | "install", "update", "chrome_update", "shared_module_update" |
| details.previousVersion | string | Previous version (if reason is "update") |

### onMessage
**Fired when**: A message is sent from either an extension process or a content script.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| message | any | The message sent |
| sender | MessageSender | Details about the message sender |
| sendResponse | function | Function to call to send a response |

#### Code Examples
```javascript
browser.runtime.onMessage.addListener((request, sender, sendResponse) => {
  if (request.action === "ping") {
    sendResponse({response: "pong"});
  }
});
```

### onConnect
**Fired when**: A connection is made with either an extension process or a content script.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| port | Port | Port object for the new connection |

### onSuspend
**Fired when**: Sent to the event page just before the extension is unloaded.

### onUpdateAvailable
**Fired when**: An update is available, but isn't installed immediately because the extension is currently running.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| details | object | Update details |
| details.version | string | Version of the available update |

## Related APIs
- `tabs` - For tab-related messaging and management
- `storage` - For persisting extension data
- `permissions` - For runtime permission management
- `webRequest` - For intercepting network requests
