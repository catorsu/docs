# pkcs11

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pkcs11
- **Version**: Current as of June 2025

## Overview

The pkcs11 API enables an extension to enumerate PKCS #11 security modules and to make them accessible to the browser as sources of keys and certificates. Starting with Firefox 58, extensions can use this API to manage PKCS #11 modules for cryptographic operations.

There are two environmental prerequisites for using this API:
- One or more PKCS #11 modules must be installed on the user's computer
- For each installed PKCS #11 module, there must be a native manifest file that enables the browser to locate the module

## Permissions
- `pkcs11` - required to use this API

## Types

### Token
Represents a token in a PKCS #11 slot with the following properties:
- **name**: string - Name of the token
- **manufacturer**: string - Name of the token's manufacturer  
- **HWVersion**: string - Hardware version as PKCS #11 version number (e.g., "1.0")
- **FWVersion**: string - Firmware version as PKCS #11 version number (e.g., "1.0")
- **serial**: string - Serial number whose format is defined by the token specification
- **isLoggedIn**: boolean - True if the token is logged on, false otherwise

## Methods

### getModuleSlots()
**Syntax**: `browser.pkcs11.getModuleSlots(name)`

Enumerate a module's slots. Returns an array containing one entry for each slot with the slot's name and token information if present.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | Yes | - | Name of the module. Must match the name property in the PKCS #11 manifest |

#### Returns
- **Type**: `Promise<Array<Object>>`
- **Description**: Array of objects with 'name' (slot name) and 'token' (Token object or null) properties

#### Code Examples
```javascript
function onInstalled() {
  return browser.pkcs11.getModuleSlots("my_module");
}

function onGotSlots(slots) {
  for (const slot of slots) {
    console.log(`Slot: ${slot.name}`);
    if (slot.token) {
      console.log(`Contains token: ${slot.token.name}`);
    } else {
      console.log("Is empty");
    }
  }
}

browser.pkcs11.installModule("my_module").then(onInstalled).then(onGotSlots);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pkcs11/getModuleSlots#examples

### installModule()
**Syntax**: `browser.pkcs11.installModule(name, flags)`

Installs the named PKCS #11 module, making it available to Firefox.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | Yes | - | Name of the module to install. Must match the name property in the PKCS #11 manifest |
| flags | integer | No | - | Flags to pass to the module |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise fulfilled with no arguments once the module is installed

#### Code Examples
```javascript
function onInstalled() {
  return browser.pkcs11.getModuleSlots("my_module");
}

function onGotSlots(slots) {
  for (const slot of slots) {
    console.log(`Slot: ${slot.name}`);
    if (slot.token) {
      console.log(`Contains token: ${slot.token.name}`);
    } else {
      console.log("Is empty");
    }
  }
}

browser.pkcs11.installModule("my_module").then(onInstalled).then(onGotSlots);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pkcs11/installModule#examples

### isModuleInstalled()
**Syntax**: `browser.pkcs11.isModuleInstalled(name)`

Checks whether the named PKCS #11 module is currently installed in Firefox.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | Yes | - | Name of the module to check |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the module is installed, false otherwise

#### Code Examples
```javascript
function logIsInstalled(isInstalled) {
  console.log(`Module is installed: ${isInstalled}`);
}

browser.pkcs11.isModuleInstalled("pkcs11_module").then(logIsInstalled);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pkcs11/isModuleInstalled#examples

### uninstallModule()
**Syntax**: `browser.pkcs11.uninstallModule(name)`

Uninstalls the named PKCS #11 module from Firefox.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | Yes | - | Name of the module to uninstall. Must match the name property in the PKCS #11 manifest |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise fulfilled with no arguments once the module is uninstalled

#### Code Examples
```javascript
browser.pkcs11.uninstallModule("pkcs11_module");
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/pkcs11/uninstallModule#examples

## Events
No events are defined for this API.

## Related APIs
- `nativeMessaging` - For communicating with native applications that may use PKCS #11
- `permissions` - For requesting the pkcs11 permission
