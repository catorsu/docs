# UserScripts

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts
- **Version**: Firefox WebExtensions API (Manifest V3)

## Overview

Use this API to register user scripts, third-party scripts designed to manipulate webpages or provide new features. Registering a user script instructs the browser to attach the script to pages that match the URL patterns specified during registration. This API offers capabilities similar to scripting but with features suited to handling third-party scripts.

## Permissions
- **Required**: `userScripts` permission and `host_permissions` for sites where you want to run scripts
- **Firefox**: `userScripts` is an optional-only permission declared in `optional_permissions` manifest key
- **Chrome**: Install time permission that requires users to enable developer environment

## Types

### ExecutionWorld
| Value | Description |
|-------|-------------|
| `"MAIN"` | Web page execution environment, shared with host page without isolation |
| `"USER_SCRIPT"` | Default isolated execution environment for user scripts |

### RegisteredUserScript
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | string | Yes | - | Unique ID for the user script (must not start with '_') |
| js | ScriptSource[] | Yes | - | Array of scripts to inject into matching pages |
| matches | string[] | No* | - | Match patterns for pages to run script in |
| includeGlobs | string[] | No* | - | Glob patterns for pages to run script in |
| excludeMatches | string[] | No | - | Patterns to exclude from execution |
| excludeGlobs | string[] | No | - | Glob patterns to exclude from execution |
| allFrames | boolean | No | false | Whether to inject into all frames or just top frame |
| runAt | string | No | "document_idle" | When to inject the script |
| world | ExecutionWorld | No | "USER_SCRIPT" | Execution environment for the script |
| worldId | string | No | "" | ID of user script world (only valid for USER_SCRIPT) |

*Either `matches` or `includeGlobs` must be specified

### ScriptSource
| Property | Type | Required | Description |
|----------|------|----------|-------------|
| code | string | No* | JavaScript code to execute |
| file | string | No* | Path to JavaScript file to execute |

*Either `code` or `file` must be specified

### UserScriptFilter
| Property | Type | Required | Description |
|----------|------|----------|-------------|
| ids | string[] | No | Array of script IDs to filter by |

### WorldProperties
| Property | Type | Required | Description |
|----------|------|----------|-------------|
| csp | string | No | Content Security Policy for USER_SCRIPT world |
| messaging | boolean | No | Whether to enable messaging APIs |

## Methods

### configureWorld()
**Syntax**: `userScripts.configureWorld(properties)`

Configures a USER_SCRIPT execution environment for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| properties | WorldProperties | Yes | - | Configuration for the world |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when world is configured

#### Code Examples
```javascript
// Enable messaging for user scripts
browser.userScripts.configureWorld({
  messaging: true
});

// Set custom CSP
browser.userScripts.configureWorld({
  csp: "script-src 'self'"
});

// Configure both messaging and CSP
browser.userScripts.configureWorld({
  messaging: true,
  csp: "script-src 'self' 'unsafe-inline'"
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts

### register()
**Syntax**: `userScripts.register(scripts)`

Registers user scripts for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| scripts | RegisteredUserScript[] | Yes | - | Array of user scripts to register |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise fulfilled with no arguments if all scripts are registered

#### Code Examples
```javascript
await browser.userScripts.register([
  {
    id: "myScript",
    worldId: "myScriptId",
    js: [{ code: "console.log('Hello world!');" }],
    matches: ["*://example.com/*"],
    runAt: "document_start"
  }
]);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts/register

### getScripts()
**Syntax**: `userScripts.getScripts(filter)`

Returns user scripts registered by the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | UserScriptFilter | No | - | Optional filter to limit returned scripts |

#### Returns
- **Type**: `Promise<RegisteredUserScript[]>`
- **Description**: Array of registered user scripts matching the filter

#### Code Examples
```javascript
// Get all scripts
const allScripts = await browser.userScripts.getScripts();

// Get specific scripts by ID
const specificScripts = await browser.userScripts.getScripts({
  ids: ["script1", "script2"]
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts/getScripts

### update()
**Syntax**: `userScripts.update(scripts)`

Updates user scripts registered by the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| scripts | RegisteredUserScript[] | Yes | - | Array of script updates |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when scripts are updated

#### Code Examples
```javascript
// Update script code
await browser.userScripts.update([
  {
    id: "myScript",
    js: [{ code: "console.log('Updated script!');" }]
  }
]);

// Update matches
await browser.userScripts.update([
  {
    id: "myScript", 
    matches: ["*://newsite.com/*"]
  }
]);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts/update

### unregister()
**Syntax**: `userScripts.unregister(filter)`

Unregisters user scripts registered by the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | UserScriptFilter | No | - | Optional filter for scripts to unregister |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when scripts are unregistered

#### Code Examples
```javascript
// Unregister all scripts
await browser.userScripts.unregister();

// Unregister specific scripts
await browser.userScripts.unregister({
  ids: ["script1", "script2"]
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts

### getWorldConfigurations()
**Syntax**: `userScripts.getWorldConfigurations()`

Returns all the extension's registered world configurations.

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object containing world configurations

### resetWorldConfiguration()
**Syntax**: `userScripts.resetWorldConfiguration(worldId)`

Resets the configuration for a USER_SCRIPT world registered by the extension.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| worldId | string | Yes | ID of the world to reset |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when world is reset

## Execution Worlds

User scripts can execute in two different environments:

### USER_SCRIPT World
- **Isolation**: Isolated from page context and other USER_SCRIPT worlds
- **APIs**: No access to extension APIs (except messaging if configured)
- **CSP**: Can be configured with custom Content Security Policy
- **WorldId**: Supports custom world identifiers for isolation

### MAIN World
- **Isolation**: Shared with host page, no isolation
- **APIs**: No access to extension APIs
- **Visibility**: Accessible to host pages and other extensions
- **Warning**: Web pages can detect and interfere with executed code

## Messaging

User scripts can communicate with extensions using dedicated messaging APIs:

### Setup
```javascript
// Must call before registering scripts
browser.userScripts.configureWorld({
  messaging: true
});
```

### Sending Messages from User Scripts
```javascript
// In user script
browser.runtime.sendMessage({data: "from user script"});
browser.runtime.connect({name: "user-script-port"});
```

### Receiving Messages in Extension
```javascript
// In extension background script
browser.runtime.onUserScriptMessage.addListener((message, sender) => {
  console.log("Message from user script:", message);
});

browser.runtime.onUserScriptConnect.addListener((port) => {
  console.log("Connection from user script:", port.name);
});
```

## Extension Updates

User scripts are cleared when an extension updates. To restore them:

```javascript
browser.runtime.onInstalled.addListener((details) => {
  if (details.reason === "update") {
    // Re-register your user scripts here
    registerUserScripts();
  }
});
```

## Related APIs
- `runtime.onUserScriptMessage` - Receive messages from user scripts
- `runtime.onUserScriptConnect` - Handle connections from user scripts  
- `scripting` - Similar injection capabilities for extension scripts
- `permissions` - Check and request userScripts permission

## Notes
- Requires Manifest V3 in Firefox
- Scripts must include either `matches` or `includeGlobs` array
- WorldId values with leading underscores are reserved
- Maximum worldId length is 256 characters
- Configuration persists across browser sessions
