# Types

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/types
- **Version**: Firefox WebExtensions API

## Overview

Defines the BrowserSetting type, which is used to represent a browser setting. This API provides the foundational type system for browser configuration management in WebExtensions.

## Types

### BrowserSetting

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| value | varies | Yes | - | The current value of the setting (type depends on specific setting) |
| levelOfControl | string | Yes | - | How the setting is currently controlled |

#### Level of Control Values
- `"not_controllable"` - Extensions are not allowed to modify this setting
- `"controlled_by_other_extensions"` - Another extension has modified this setting  
- `"controllable_by_this_extension"` - This extension can modify the setting
- `"controlled_by_this_extension"` - This extension has already modified the setting

## Methods

### get()
**Syntax**: `BrowserSetting.get(details)`

Gets the current value of the browser setting and enumeration indicating how the setting's value is currently controlled.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Empty object |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Promise that resolves to an object with `value` and `levelOfControl` properties

#### Code Examples
```javascript
let getting = browser.privacy.network.networkPredictionEnabled.get({});
getting.then((got) => {
  console.log(`Value: ${got.value}`);
  console.log(`Control: ${got.levelOfControl}`);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/types/BrowserSetting/get

### set()
**Syntax**: `BrowserSetting.set(details)`

Sets the browser setting to a new value. Extensions are given precedence based on installation order, with more recent installations having higher precedence.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing the new value |
| details.value | varies | Yes | - | The new value for the setting |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the setting was modified, false otherwise

#### Code Examples
```javascript
function onSet(result) {
  if (result) {
    console.log("Value was updated");
  } else {
    console.log("Value was not updated");
  }
}

browser.browserAction.onClicked.addListener(() => {
  let setting = browser.privacy.websites.hyperlinkAuditingEnabled.set({
    value: false,
  });
  setting.then(onSet);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/types/BrowserSetting/set

### clear()
**Syntax**: `BrowserSetting.clear(details)`

Clears any changes the extension has made to the browser setting, reverting to previous value and giving up control of the setting.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Empty object |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the setting was cleared, false otherwise

#### Code Examples
```javascript
function onCleared(result) {
  if (result) {
    console.log("Setting was cleared");
  } else {
    console.log("Setting was not cleared");
  }
}

let clearing = browser.privacy.network.webRTCIPHandlingPolicy.clear({});
clearing.then(onCleared);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/types/BrowserSetting/clear

## Events

### onChange
**Fired when**: The setting's value changes

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| details.value | varies | The new value of the setting |
| details.levelOfControl | string | How the setting is currently controlled |

#### Code Examples
```javascript
BrowserSetting.onChange.addListener(listener)
BrowserSetting.onChange.removeListener(listener)
BrowserSetting.onChange.hasListener(listener)

// Example listener function
function handleChange(details) {
  console.log(`New value: ${details.value}`);
  console.log(`Control level: ${details.levelOfControl}`);
}
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/types/BrowserSetting/onChange

## Related APIs
- `browserSettings` - Provides specific browser settings as BrowserSetting objects
- `privacy` - Contains privacy-related settings using BrowserSetting type

## Notes
- Based on Chromium's chrome.types API
- Does not distinguish between normal and private browsing windows
- Private browsing scope options are not implemented
- On Firefox, onChange doesn't fire for changes made through about:config
