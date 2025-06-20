# scripting

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/scripting
- **Version**: Current as of June 2025

## Overview

Inserts JavaScript and CSS into websites. This API offers two approaches: one-off injections using executeScript(), insertCSS(), and removeCSS(), and dynamic content script registration using registerContentScripts() and related methods.

Note: Chrome restricts this API to Manifest V3. Firefox and Safari support this API in both Manifest V2 and V3.

## Permissions
- `scripting` - required to use this API
- Host permissions for target tabs where JavaScript or CSS is injected
- `activeTab` - alternative for temporary permission in active tab (still requires "scripting" permission)

## Types

### InjectionTarget
Details of an injection target:
- **tabId**: number - ID of the tab to inject into
- **frameIds**: array - Array of frame IDs to inject into (optional)
- **allFrames**: boolean - Whether to inject into all frames (optional)
- **documentIds**: array - Array of document IDs to inject into (optional)

### RegisteredContentScript
Details of a content script to be registered:
- **id**: string - Unique identifier for the script
- **matches**: array - URL patterns where script should run
- **excludeMatches**: array - URL patterns to exclude (optional)
- **js**: array - JavaScript files to inject (optional)
- **css**: array - CSS files to inject (optional)
- **runAt**: string - When to inject ("document_start", "document_end", "document_idle")
- **allFrames**: boolean - Whether to inject into all frames
- **matchOriginAsFallback**: boolean - Match origin as fallback (optional)
- **world**: string - Execution environment ("ISOLATED", "MAIN")

### ExecutionWorld
Specifies the execution environment:
- **"ISOLATED"** - Isolated world (default, recommended)
- **"MAIN"** - Main world (page's JavaScript context)

### ContentScriptFilter
Specifies the IDs of scripts to retrieve or unregister:
- **ids**: array - Array of script IDs to filter

## Methods

### executeScript()
**Syntax**: `browser.scripting.executeScript(injection)`

Injects JavaScript code into a page.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| injection | object | Yes | - | Injection details |
| injection.target | InjectionTarget | Yes | - | Target for injection |
| injection.files | array | No | - | Array of JavaScript files to inject |
| injection.func | function | No | - | Function to inject and execute |
| injection.args | array | No | - | Arguments for the function |
| injection.world | ExecutionWorld | No | "ISOLATED" | Execution environment |

#### Returns
- **Type**: `Promise<array>`
- **Description**: Promise that resolves to array of injection results

#### Code Examples
```javascript
// Inject a function
browser.scripting.executeScript({
  target: { tabId: 123 },
  func: () => document.title,
}).then(results => {
  console.log('Page title:', results[0].result);
});

// Inject a file
browser.scripting.executeScript({
  target: { tabId: 123 },
  files: ['content-script.js']
});
```

### insertCSS()
**Syntax**: `browser.scripting.insertCSS(injection)`

Injects CSS into a page.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| injection | object | Yes | - | CSS injection details |
| injection.target | InjectionTarget | Yes | - | Target for injection |
| injection.files | array | No | - | Array of CSS files to inject |
| injection.css | string | No | - | CSS code to inject |
| injection.origin | string | No | "AUTHOR" | CSS origin ("AUTHOR" or "USER") |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when CSS is injected

#### Code Examples
```javascript
// Inject CSS code
browser.scripting.insertCSS({
  target: { tabId: 123 },
  css: 'body { background-color: red; }'
});

// Inject CSS file
browser.scripting.insertCSS({
  target: { tabId: 123 },
  files: ['styles.css']
});
```

### removeCSS()
**Syntax**: `browser.scripting.removeCSS(injection)`

Removes CSS which was previously injected into a page by an insertCSS() call.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| injection | object | Yes | - | CSS removal details |
| injection.target | InjectionTarget | Yes | - | Target for removal |
| injection.files | array | No | - | Array of CSS files to remove |
| injection.css | string | No | - | CSS code to remove |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when CSS is removed

### registerContentScripts()
**Syntax**: `browser.scripting.registerContentScripts(scripts)`

Registers content scripts for future page loads.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| scripts | array | Yes | - | Array of RegisteredContentScript objects |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when scripts are registered

#### Code Examples
```javascript
browser.scripting.registerContentScripts([{
  id: 'my-script',
  matches: ['https://example.com/*'],
  js: ['content-script.js'],
  runAt: 'document_end'
}]);
```

### getRegisteredContentScripts()
**Syntax**: `browser.scripting.getRegisteredContentScripts(filter)`

Gets a list of registered content scripts.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | ContentScriptFilter | No | - | Filter for specific script IDs |

#### Returns
- **Type**: `Promise<array>`
- **Description**: Promise that resolves to array of RegisteredContentScript objects

#### Code Examples
```javascript
// Get all registered scripts
browser.scripting.getRegisteredContentScripts().then(scripts => {
  console.log('Registered scripts:', scripts);
});

// Get specific scripts
browser.scripting.getRegisteredContentScripts({
  ids: ['my-script']
}).then(scripts => {
  console.log('Found scripts:', scripts);
});
```

### unregisterContentScripts()
**Syntax**: `browser.scripting.unregisterContentScripts(filter)`

Unregisters one or more content scripts.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | ContentScriptFilter | No | - | Filter for script IDs to unregister (omit to unregister all) |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when scripts are unregistered

#### Code Examples
```javascript
// Unregister specific scripts
browser.scripting.unregisterContentScripts({
  ids: ['my-script']
});

// Unregister all scripts
browser.scripting.unregisterContentScripts();
```

### updateContentScripts()
**Syntax**: `browser.scripting.updateContentScripts(scripts)`

Updates one or more content scripts already registered.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| scripts | array | Yes | - | Array of RegisteredContentScript objects with updates |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when scripts are updated

## Events
No events are defined for this API.

## Related APIs
- `tabs` - For getting tab information for injection targets
- `activeTab` - Permission for temporary access to active tab
- `contentScripts` - Manifest V2 equivalent for registering content scripts
- `webNavigation` - For listening to page navigation events
