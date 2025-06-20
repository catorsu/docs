# management

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management
- **Version**: WebExtensions API

## Overview

Get information about installed add-ons. With the management API you can:
- Get information about installed add-ons
- Enable/disable add-ons
- Uninstall add-ons
- Find out which permission warnings are given for particular add-ons or manifests
- Get notifications of add-ons being installed, uninstalled, enabled, or disabled

Most operations require the "management" API permission. Operations that don't provide access to other add-ons (like `getSelf()` and `uninstallSelf()`) don't require this permission.

## Permissions
- `management` - required for most operations (accessing other extensions)
- No permission needed for: `getSelf()`, `uninstallSelf()`

## Types

### ExtensionInfo
Object containing information about an installed add-on.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `description` | string | Yes | - | Add-on's description from manifest.json |
| `disabledReason` | string | No | - | If disabled, the reason: "unknown" or "permissions_increase" |
| `enabled` | boolean | Yes | - | Whether the add-on is currently enabled |
| `homepageUrl` | string | No | - | Homepage URL from manifest.json |
| `hostPermissions` | array of string | Yes | - | Add-on's host permissions |
| `icons` | array of object | No | - | Icon information: [{size: number, url: string}] |
| `id` | string | Yes | - | The add-on's ID |
| `installType` | string | Yes | - | How installed: "admin", "development", "normal", "sideload", "other" |
| `mayDisable` | boolean | Yes | - | Whether user can disable/uninstall this add-on |
| `name` | string | Yes | - | Add-on's name from manifest.json |
| `offlineEnabled` | boolean | Yes | - | Whether add-on claims to support offline |
| `optionsUrl` | string | No | - | Relative URL to options page |
| `permissions` | array of string | Yes | - | Add-on's API permissions |
| `shortName` | string | No | - | Short version of name from manifest.json |
| `type` | string | Yes | - | Type: "extension", "hosted_app", "packaged_app", "legacy_packaged_app", "theme" |
| `updateUrl` | string | No | - | URL for updates from browser_specific_settings |
| `version` | string | Yes | - | Version from manifest.json |
| `versionName` | string | No | - | Descriptive version name from manifest.json |

## Methods

### getAll()
Returns information about all installed add-ons.

**Syntax**: `browser.management.getAll()`

#### Parameters
None

#### Returns
- **Type**: `Promise<ExtensionInfo[]>`
- **Description**: Array of ExtensionInfo objects, one for each installed add-on

#### Code Examples
```javascript
function gotAll(infoArray) {
  for (const info of infoArray) {
    if (info.type === "extension") {
      console.log(info.name);
      console.log(`Version: ${info.version}`);
      console.log(`Enabled: ${info.enabled}`);
    }
  }
}

let gettingAll = browser.management.getAll();
gettingAll.then(gotAll);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/getAll

### get()
Returns information about a particular add-on, given its ID.

**Syntax**: `browser.management.get(id)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `id` | string | Yes | - | ID of the add-on to retrieve |

#### Returns
- **Type**: `Promise<ExtensionInfo>`
- **Description**: ExtensionInfo object for the specified add-on

**Errors**: Promise rejected if no extension with given ID exists or caller lacks access

#### Code Examples
```javascript
let id = "my-add-on@example.com";

function got(info) {
  console.log(info.name);
  console.log(info.description);
}

let getting = browser.management.get(id);
getting.then(got);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/get

### getSelf()
Returns information about the calling add-on.

**Syntax**: `browser.management.getSelf()`

#### Parameters
None

#### Returns
- **Type**: `Promise<ExtensionInfo>`
- **Description**: ExtensionInfo object for the calling add-on

**Note**: Does not require "management" permission

#### Code Examples
```javascript
function gotSelf(info) {
  console.log(`Add-on name: ${info.name}`);
  console.log(`Version: ${info.version}`);
}

const gettingSelf = browser.management.getSelf();
gettingSelf.then(gotSelf);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/getSelf

### install()
Installs a particular theme, given its URL at addons.mozilla.org.

**Syntax**: `browser.management.install(options)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `options` | object | Yes | - | Installation options |
| `options.url` | string | Yes | - | URL of the theme at addons.mozilla.org |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with `id` property containing installed extension ID

**Note**: This function is typically used for installing themes from AMO

### uninstall()
Uninstalls a particular add-on, given its ID.

**Syntax**: `browser.management.uninstall(id, options)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `id` | string | Yes | - | ID of the add-on to uninstall |
| `options` | object | No | {} | Uninstall options |
| `options.showConfirmDialog` | boolean | No | true for other add-ons | Whether to show confirmation dialog |

**Note**: Confirmation dialog is always shown when uninstalling other add-ons, regardless of `showConfirmDialog`

#### Returns
- **Type**: `Promise<void>`
- **Description**: Rejected if user cancels uninstallation

#### Code Examples
```javascript
let id = "other-addon@example.com";

function onCanceled(error) {
  console.log(`Uninstall canceled: ${error}`);
}

function onUninstalled() {
  console.log("Uninstalled successfully");
}

let uninstalling = browser.management.uninstall(id, {
  showConfirmDialog: true
});

uninstalling.then(onUninstalled, onCanceled);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/uninstall

### uninstallSelf()
Uninstalls the calling add-on.

**Syntax**: `browser.management.uninstallSelf(options)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `options` | object | No | {} | Uninstall options |
| `options.showConfirmDialog` | boolean | No | false | Whether to show confirmation dialog |
| `options.dialogMessage` | string | No | - | Extra message for confirmation dialog |

**Note**: Does not require "management" permission

#### Returns
- **Type**: `Promise<void>`
- **Description**: Rejected if user cancels uninstallation

#### Code Examples
```javascript
function onCanceled(error) {
  console.log(`Canceled: ${error}`);
}

let uninstalling = browser.management.uninstallSelf({
  showConfirmDialog: true,
  dialogMessage: "Are you sure you want to remove this extension?"
});

uninstalling.then(null, onCanceled);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/uninstallSelf

### setEnabled()
Enables or disables the given add-on.

**Syntax**: `browser.management.setEnabled(id, enabled)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `id` | string | Yes | - | ID of the add-on |
| `enabled` | boolean | Yes | - | Whether to enable (true) or disable (false) |

**Notes**:
- Must usually be called in response to user action (e.g., button click)
- Browser may ask user to confirm the change

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when add-on has been enabled/disabled

#### Code Examples
```javascript
let id = "my-addon@example.com";

function toggleEnabled(id) {
  let getting = browser.management.get(id);
  getting.then((info) => {
    browser.management.setEnabled(id, !info.enabled);
  });
}

toggleEnabled(id);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/management/setEnabled

### getPermissionWarningsById()
Get the set of permission warnings for a particular add-on.

**Syntax**: `browser.management.getPermissionWarningsById(id)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `id` | string | Yes | - | ID of the add-on |

#### Returns
- **Type**: `Promise<string[]>`
- **Description**: Array of permission warning strings

### getPermissionWarningsByManifest()
Get the set of permission warnings that would be displayed for the given manifest string.

**Syntax**: `browser.management.getPermissionWarningsByManifest(manifestStr)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `manifestStr` | string | Yes | - | Manifest JSON string |

#### Returns
- **Type**: `Promise<string[]>`
- **Description**: Array of permission warning strings

## Events

### onInstalled
Fired when an add-on is installed.

**Syntax**: `browser.management.onInstalled.addListener(listener)`

**Listener receives**:
- `info` (ExtensionInfo): Information about the installed add-on

#### Code Examples
```javascript
browser.management.onInstalled.addListener((info) => {
  console.log(`${info.name} was installed`);
  console.log(`Type: ${info.type}`);
  console.log(`Version: ${info.version}`);
});
```

### onUninstalled
Fired when an add-on is uninstalled.

**Syntax**: `browser.management.onUninstalled.addListener(listener)`

**Listener receives**:
- `info` (ExtensionInfo): Information about the uninstalled add-on

#### Code Examples
```javascript
browser.management.onUninstalled.addListener((info) => {
  console.log(`${info.name} was uninstalled`);
});
```

### onEnabled
Fired when an add-on is enabled.

**Syntax**: `browser.management.onEnabled.addListener(listener)`

**Listener receives**:
- `info` (ExtensionInfo): Information about the enabled add-on

#### Code Examples
```javascript
browser.management.onEnabled.addListener((info) => {
  console.log(`${info.name} was enabled`);
});
```

### onDisabled
Fired when an add-on is disabled.

**Syntax**: `browser.management.onDisabled.addListener(listener)`

**Listener receives**:
- `info` (ExtensionInfo): Information about the disabled add-on

#### Code Examples
```javascript
browser.management.onDisabled.addListener((info) => {
  console.log(`${info.name} was disabled`);
  if (info.disabledReason) {
    console.log(`Reason: ${info.disabledReason}`);
  }
});
```

## Usage Examples

### Extension Manager
```javascript
// List all extensions with enable/disable toggles
async function createExtensionManager() {
  const extensions = await browser.management.getAll();
  
  extensions
    .filter(ext => ext.type === "extension")
    .forEach(ext => {
      console.log(`${ext.name} (${ext.id})`);
      console.log(`  Enabled: ${ext.enabled}`);
      console.log(`  Version: ${ext.version}`);
      console.log(`  Can disable: ${ext.mayDisable}`);
    });
}
```

### Monitor Extension Changes
```javascript
// Track all extension state changes
browser.management.onInstalled.addListener((info) => {
  browser.notifications.create({
    type: "basic",
    iconUrl: info.icons?.[0]?.url || "icon.png",
    title: "Extension Installed",
    message: `${info.name} has been installed`
  });
});

browser.management.onUninstalled.addListener((info) => {
  console.log(`Extension removed: ${info.name}`);
});

browser.management.onEnabled.addListener((info) => {
  console.log(`Extension enabled: ${info.name}`);
});

browser.management.onDisabled.addListener((info) => {
  console.log(`Extension disabled: ${info.name}`);
});
```

## Related APIs
- `runtime` - Get information about the extension runtime
- `permissions` - Query and modify extension permissions
- `notifications` - Show notifications about extension changes