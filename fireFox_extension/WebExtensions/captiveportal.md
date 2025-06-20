# CaptivePortal

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/captivePortal
- **Version**: Firefox 52+

## Overview
Determine the captive portal state of the user's connection. A captive portal is a web page displayed when a user first connects to a Wi-Fi network. The user provides information or acts on the captive portal web page to gain broader access to network resources, such as accepting terms and conditions or making a payment.

## Permissions
- `captivePortal` - required

## Types
### State
| Value | Description |
|-------|-------------|
| "unknown" | The captive portal state is unknown |
| "not_captive" | The user is not behind a captive portal |
| "unlocked_portal" | The user is behind a captive portal but has been granted access |
| "locked_portal" | The user is behind a captive portal and has not been granted access |

## Properties
### canonicalURL
**Type**: `string`
**Description**: Return the canonical URL of the captive-portal detection page. Read-only.

## Methods
### getLastChecked()
**Syntax**: `browser.captivePortal.getLastChecked()`

Returns the time, in milliseconds, since the last request was completed.

#### Parameters
None

#### Returns
- **Type**: `Promise<number>`
- **Description**: Fulfilled with the time in milliseconds since the last completed request

#### Code Examples
No code examples in source documentation

### getState()
**Syntax**: `browser.captivePortal.getState()`

Returns the portal state.

#### Parameters
None

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with one of: "unknown", "not_captive", "unlocked_portal", or "locked_portal"

#### Code Examples
No code examples in source documentation

## Events
### onConnectivityAvailable
**Fired when**: The captive portal service determines that the user can connect to the internet

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| status | string | The connectivity status |

### onStateChanged
**Fired when**: The captive portal state changes

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| details | object | Object containing the new state |
| details.state | string | The new captive portal state |

## Related APIs
- No directly related APIs listed