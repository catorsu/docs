# privacy

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/privacy
- **Version**: Current as of June 2025

## Overview

Access and modify various privacy-related browser settings. The privacy API enables extensions to control privacy and security settings across three main categories: network settings, browser services, and website behavior. All properties are BrowserSetting objects that provide get(), set(), and onChange() methods.

To use the privacy API, you must have the "privacy" API permission in your manifest.

## Permissions
- `privacy` - required to access privacy settings

## Types
All privacy settings use the **types.BrowserSetting** object, which provides:
- **get()** - Retrieve current setting value
- **set()** - Change the setting value
- **onChange** - Listen for setting changes

## Properties

### privacy.network
Access and modify privacy settings relating to the network.

#### Properties
| Property | Type | Description |
|----------|------|-------------|
| networkPredictionEnabled | BrowserSetting<boolean> | If true, browser attempts to speed up browsing by pre-resolving DNS entries and prerendering sites |
| peerConnectionEnabled | BrowserSetting<boolean> | If false, RTCPeerConnection interface is disabled (getUserMedia() not affected) |
| webRTCIPHandlingPolicy | BrowserSetting<string> | Controls WebRTC traffic routing and local address information exposure |
| globalPrivacyControl | BrowserSetting<boolean> | Read-only. Indicates if browser sends Global Privacy Control signals |

#### Code Examples
```javascript
function onSet(result) {
  if (result) {
    console.log("success");
  } else {
    console.log("failure");
  }
}

browser.browserAction.onClicked.addListener(() => {
  let getting = browser.privacy.network.webRTCIPHandlingPolicy.get({});
  getting.then((got) => {
    console.log(got.value);
    if (
      got.levelOfControl === "controlled_by_this_extension" ||
      got.levelOfControl === "controllable_by_this_extension"
    ) {
      let setting = browser.privacy.network.webRTCIPHandlingPolicy.set({
        value: "default_public_interface_only",
      });
      setting.then(onSet);
    } else {
      console.log("Not able to set webRTCIPHandlingPolicy");
    }
  });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/privacy/network#examples

### privacy.services
Access and modify privacy settings relating to the services provided by the browser or third parties.

#### Properties
| Property | Type | Description |
|----------|------|-------------|
| passwordSavingEnabled | BrowserSetting<boolean> | If true, browser's password manager will offer to store passwords. Defaults to true |

#### Code Examples
```javascript
function onSet(result) {
  if (result) {
    console.log("success");
  } else {
    console.log("failure");
  }
}

let getting = browser.privacy.services.passwordSavingEnabled.get({});
getting.then((got) => {
  console.log(got.value);
  if (
    got.levelOfControl === "controlled_by_this_extension" ||
    got.levelOfControl === "controllable_by_this_extension"
  ) {
    let setting = browser.privacy.services.passwordSavingEnabled.set({
      value: false,
    });
    setting.then(onSet);
  } else {
    console.log("Not able to set passwordSavingEnabled");
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/privacy/services#examples

### privacy.websites
Access and modify privacy settings relating to the behavior of websites.

#### Properties
| Property | Type | Description |
|----------|------|-------------|
| thirdPartyCookiesAllowed | BrowserSetting<string> | Controls third-party cookie behavior. Values: "allow_all", "block_all", "allow_visited" |
| hyperlinkAuditingEnabled | BrowserSetting<boolean> | If true, browser sends auditing pings when websites use ping attribute |
| protectedContentEnabled | BrowserSetting<boolean> | Windows only. If true, browser provides unique ID to plugins for protected content |
| referrersEnabled | BrowserSetting<boolean> | If enabled, browser sends referer headers with requests |
| resistFingerprinting | BrowserSetting<boolean> | If true, browser reports generic spoofed information for fingerprinting protection |
| firstPartyIsolate | BrowserSetting<boolean> | If true, associates all third-party data with top-level domain to prevent tracking |

#### Code Examples
```javascript
function onSet(result) {
  if (result) {
    console.log("success");
  } else {
    console.log("failure");
  }
}

browser.browserAction.onClicked.addListener(() => {
  let getting = browser.privacy.websites.hyperlinkAuditingEnabled.get({});
  getting.then((got) => {
    console.log(got.value);
    if (
      got.levelOfControl === "controlled_by_this_extension" ||
      got.levelOfControl === "controllable_by_this_extension"
    ) {
      let setting = browser.privacy.websites.hyperlinkAuditingEnabled.set({
        value: true,
      });
      setting.then(onSet);
    } else {
      console.log("Not able to set hyperlinkAuditingEnabled");
    }
  });
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/privacy/websites#examples

## Events
All privacy settings inherit onChange events from the BrowserSetting type for monitoring setting changes.

## Related APIs
- `types.BrowserSetting` - Base type for all privacy settings
- `permissions` - For requesting the privacy permission
- `browserSettings` - For general browser configuration settings
