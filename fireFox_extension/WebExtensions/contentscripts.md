# ContentScripts

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/contentScripts
- **Version**: Firefox 59+ (Manifest V2 only)

## Overview
Use this API to register content scripts. Registering a content script instructs the browser to insert the given content scripts into pages that match the given URL patterns.

Note: When using Manifest V3 or higher, use scripting.registerContentScripts() to register scripts.

This API is very similar to the "content_scripts" manifest.json key, except that with "content_scripts", the set of content scripts and associated patterns is fixed at install time. With the contentScripts API, an extension can register and unregister scripts at runtime.

## Permissions
- No API permission required
- Host permissions required for any URL patterns

## Types
### RegisteredContentScript
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| unregister | function | Yes | - | Method to unregister the content scripts |

### ContentScriptOptions
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| matches | Array<string> | Yes | - | Array of match patterns specifying which pages this content script will be injected into |
| excludeMatches | Array<string> | No | - | Array of match patterns specifying pages this content script will NOT be injected into |
| includeGlobs | Array<string> | No | - | Applied after matches to include only URLs that also match this glob |
| excludeGlobs | Array<string> | No | - | Applied after matches to exclude URLs that match this glob |
| css | Array<object> | No | - | List of CSS files to inject |
| js | Array<object> | No | - | List of JavaScript files to inject |
| allFrames | boolean | No | false | If true, inject into all frames, not just the top frame |
| matchAboutBlank | boolean | No | false | If true, inject into about:blank and about:srcdoc frames |
| runAt | string | No | "document_idle" | When to inject the scripts ("document_start", "document_end", or "document_idle") |
| cookieStoreId | string or Array<string> | No | - | Restrict injection to specific cookie store IDs |

## Methods
### register()
**Syntax**: `browser.contentScripts.register(contentScriptOptions)`

Registers the given content scripts.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| contentScriptOptions | ContentScriptOptions | Yes | - | Object defining the content scripts to register |

#### Returns
- **Type**: `Promise<RegisteredContentScript>`
- **Description**: Fulfilled with a RegisteredContentScript object that can be used to unregister the scripts

#### Code Examples
```javascript
const contentScriptOptions = {
  matches: ["*://*.example.com/*"],
  js: [
    {file: "content-script.js"}
  ],
  runAt: "document_idle"
};

browser.contentScripts.register(contentScriptOptions)
  .then((registeredContentScript) => {
    // Store reference to unregister later if needed
  });
```

### RegisteredContentScript.unregister()
**Syntax**: `registeredContentScript.unregister()`

Unregisters the content scripts represented by this object.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the content scripts have been unregistered

#### Code Examples
```javascript
let registered;

// Register scripts
browser.contentScripts.register({
  matches: ["*://*.example.com/*"],
  js: [{file: "content-script.js"}]
}).then(reg => {
  registered = reg;
});

// Later, unregister
if (registered) {
  registered.unregister();
}
```

## Events
None

## Related APIs
- `scripting` - The Manifest V3 replacement for this API
- Content scripts manifest key - For statically declared content scripts
- `tabs.executeScript()` - For one-time script injection