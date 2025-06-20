# permissions

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions
- **Version**: Current as of June 2025

## Overview

Enables extensions to request extra permissions at runtime, after they have been installed. The permissions API allows extensions to ask for additional permissions at runtime that need to be listed in the `optional_permissions` manifest.json key. The main advantages include running with minimal permissions and graceful handling of permission denial instead of presenting users with an "all or nothing" choice at install time.

Starting with Firefox 84, users can manage optional permissions from the Firefox Add-ons Manager. Extensions should listen for `onAdded` and `onRemoved` events to know when users grant or revoke permissions.

## Permissions
- None required for the API itself
- Specific permissions must be listed in `optional_permissions` manifest key

## Types

### Permissions
Represents a set of permissions containing:
- **permissions**: array of API permissions (e.g., "bookmarks", "history")  
- **origins**: array of host permissions (e.g., "https://developer.mozilla.org/")

## Methods

### contains()
**Syntax**: `browser.permissions.contains(permissions)`

Check whether the extension has the permissions listed in the given permissions object.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| permissions | Permissions | Yes | - | A permissions object containing origins and/or permissions arrays |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the extension has all specified permissions, false otherwise

#### Code Examples
```javascript
// Extension permissions are: "webRequest", "tabs", "*://*.mozilla.org/*"
let testPermissions1 = {
  origins: ["*://mozilla.org/"],
  permissions: ["tabs"],
};
const testResult1 = await browser.permissions.contains(testPermissions1);
console.log(testResult1); // true

let testPermissions2 = {
  origins: ["*://mozilla.org/"],
  permissions: ["tabs", "alarms"],
};
const testResult2 = await browser.permissions.contains(testPermissions2);
console.log(testResult2); // false, "alarms" doesn't match
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/contains#examples

### getAll()
**Syntax**: `browser.permissions.getAll()`

Retrieve a permissions object containing all the permissions currently granted to the extension.

#### Parameters
None.

#### Returns
- **Type**: `Promise<Permissions>`
- **Description**: A Promise that resolves with a permissions object containing all currently granted permissions

#### Code Examples
```javascript
// Extension permissions are: "webRequest", "tabs", "*://*.mozilla.org/*"
const currentPermissions = await browser.permissions.getAll();
console.log(currentPermissions.permissions); // [ "webRequest", "tabs" ]
console.log(currentPermissions.origins); // [ "*://*.mozilla.org/*" ]
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/getAll#examples

### remove()
**Syntax**: `browser.permissions.remove(permissions)`

Ask to give up the permissions listed in the given permissions object. Permissions must come from the optional_permissions set.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| permissions | Permissions | Yes | - | A permissions object containing origins and/or permissions to remove |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the permissions are now not granted to the extension, false otherwise

#### Code Examples
```javascript
const permissionToRemove = {
  permissions: ["history"],
};

async function remove() {
  console.log("removing");
  const removed = await browser.permissions.remove(permissionToRemove);
  console.log(removed);
}

document.querySelector("#remove").addEventListener("click", remove);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/remove#examples

### request()
**Syntax**: `browser.permissions.request(permissions)`

Asks the user for the permissions listed in the permissions object. Requests can only be made in the handler for a user action. Either all permissions are granted or none are.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| permissions | Permissions | Yes | - | A permissions object containing origins and/or permissions to request |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if extension is granted the permissions, false otherwise

#### Code Examples
```javascript
const permissionsToRequest = {
  permissions: ["bookmarks", "history"],
  origins: ["https://developer.mozilla.org/"],
};

async function requestPermissions() {
  function onResponse(response) {
    if (response) {
      console.log("Permission was granted");
    } else {
      console.log("Permission was refused");
    }
    return browser.permissions.getAll();
  }
  
  const response = await browser.permissions.request(permissionsToRequest);
  const currentPermissions = await onResponse(response);
  console.log(`Current permissions:`, currentPermissions);
}

document
  .querySelector("#request")
  .addEventListener("click", requestPermissions);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/request#examples

## Events

### onAdded
**Fired when**: The extension is granted new permissions.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| permissions | Permissions | A permissions object containing the newly granted permissions and origins |

#### Code Examples
```javascript
function handleAdded(permissions) {
  console.log(`New API permissions: ${permissions.permissions}`);
  console.log(`New host permissions: ${permissions.origins}`);
}

browser.permissions.onAdded.addListener(handleAdded);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/onAdded#examples

### onRemoved
**Fired when**: Some permissions are removed from the extension.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| permissions | Permissions | A permissions object containing the removed permissions and origins |

#### Code Examples
```javascript
function handleRemoved(permissions) {
  console.log(`Removed API permissions: ${permissions.permissions}`);
  console.log(`Removed host permissions: ${permissions.origins}`);
}

browser.permissions.onRemoved.addListener(handleRemoved);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/permissions/onRemoved#examples

## Related APIs
- `optional_permissions` - Manifest key for declaring optional permissions
- `permissions` - Manifest key for declaring required permissions
- `runtime` - For handling permission-related extension lifecycle events
