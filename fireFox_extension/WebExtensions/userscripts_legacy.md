# UserScripts (Legacy)

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts_legacy
- **Version**: Firefox WebExtensions API (Manifest V2)

## Overview

**Warning**: This is documentation for the legacy userScripts API. It's available in Firefox for Manifest V2. For functionality to work with user scripts in Manifest V3 see the new userScripts API.

Use this API to register user scripts, third-party scripts designed to manipulate webpages or provide new features. This API offers similar capabilities to contentScripts but with features suited to handling third-party scripts.

## Key Features
- **Isolated Execution**: Each user script runs in an isolated sandbox within web content processes
- **Page Access**: Access to `window` and `document` globals related to the webpage
- **No Extension APIs**: User scripts cannot directly access WebExtension APIs
- **API Script Support**: Extension can provide custom APIs via API script

## Requirements
- **Manifest**: Must include `user_scripts` key in manifest.json, even if empty: `user_scripts: {}`
- **Persistence**: Register scripts from extension pages that persist as long as needed

## Types

### RegisteredUserScript
Object returned by `register()` method representing registered user scripts.

| Method | Description |
|--------|-------------|
| unregister() | Unregisters the user scripts |

### UserScriptOptions
Object passed to `register()` method representing scripts to register.

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| js | object[] | No* | JavaScript files to inject |
| js[].file | string | No* | Path to JavaScript file |
| js[].code | string | No* | JavaScript code to execute |
| matches | string[] | Yes | URL patterns where script should run |
| excludeMatches | string[] | No | URL patterns to exclude |
| includeGlobs | string[] | No | Glob patterns to include |
| excludeGlobs | string[] | No | Glob patterns to exclude |
| allFrames | boolean | No | Whether to inject into all frames |
| runAt | string | No | When to inject ("document_start", "document_end", "document_idle") |
| matchAboutBlank | boolean | No | Whether to match about:blank |
| cookieStoreId | string[] or string | No | Cookie store IDs to target |
| scriptMetadata | object | No | Arbitrary metadata for the script |

*Either `js` array with code/file or other injection method required

## Methods

### register()
**Syntax**: `userScripts.register(userScriptOptions)`

Registers user scripts for the extension.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| userScriptOptions | UserScriptOptions | Yes | Options defining the scripts to register |

#### Returns
- **Type**: `Promise<RegisteredUserScript>`
- **Description**: Promise resolved with RegisteredUserScript object

#### Code Examples
```javascript
const registeredUserScript = await browser.userScripts.register({
  js: [{code: "console.log('User script executed');"}],
  matches: ["*://example.com/*"],
  runAt: "document_end",
  allFrames: false,
  scriptMetadata: {
    name: "Example Script",
    description: "A simple example user script"
  }
});

// Later unregister
await registeredUserScript.unregister();
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts_legacy/register

## Events

### onBeforeScript
**Fired when**: Before a user script executes

Available to the API script registered in "user_scripts" to trigger export of additional APIs.

#### Code Examples
```javascript
// In API script
browser.userScripts.onBeforeScript.addListener((userScript) => {
  // Export custom APIs to user script sandbox
  const apis = {
    customAPI: {
      doSomething: () => {
        console.log("Custom API called");
      }
    }
  };
  
  // Make APIs available to user script
  return apis;
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/userScripts_legacy

## API Script Integration

The legacy userScripts API supports an API script that can provide custom APIs to user scripts:

### Manifest Declaration
```json
{
  "user_scripts": {
    "api_script": "api-script.js"
  }
}
```

### API Script Capabilities
- Executes in content script context
- Has access to extension APIs available to content scripts
- Can export custom API methods to user scripts
- Receives metadata from registered user scripts

## Migration to New API

For Manifest V3, migrate to the new userScripts API:

### Key Differences
1. **World Configuration**: New API uses `configureWorld()` for setup
2. **Messaging**: Dedicated messaging handlers in new API
3. **Registration**: Similar registration but different parameter structure
4. **Permissions**: New API uses optional permissions model

### Migration Steps
1. Update manifest to Manifest V3
2. Replace `userScripts_legacy.register()` with `userScripts.register()`
3. Update script options format
4. Configure messaging and CSP using `configureWorld()`
5. Update event handlers for messaging

## Related APIs
- `userScripts` - New Manifest V3 version of this API
- `contentScripts` - For extension-provided content scripts
- `permissions` - For managing userScripts permission

## Notes
- User scripts automatically unregister when extension page unloads
- Requires `user_scripts` manifest key even if empty
- Scripts run in isolated sandboxes
- API script can bridge user scripts to extension APIs
- Only available in Firefox Manifest V2
