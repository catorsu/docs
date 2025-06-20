# BrowserSettings

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browserSettings
- **Version**: All versions

## Overview
Enables an extension to modify certain global browser settings. Each property of this API is a BrowserSetting object, providing the ability to modify a particular setting.

Because these are global settings, it's possible for extensions to conflict. See the documentation for BrowserSetting.set() for details of how conflicts are handled.

## Permissions
- `browserSettings` - required

## Types
### BrowserSetting
Each property is a BrowserSetting object with the following methods:
- `get()` - Gets the current value of the setting
- `set()` - Sets the value of the setting
- `clear()` - Clears any modification made by the extension

## Properties
### allowPopupsForUserEvents
**Type**: `BrowserSetting`
**Description**: Determines whether code running in web pages can display popups in response to user events.

### cacheEnabled
**Type**: `BrowserSetting`
**Description**: Determines whether the browser cache is enabled or not.

### closeTabsByDoubleClick
**Type**: `BrowserSetting`
**Description**: Determines whether the selected tab can be closed with a double click.

### colorManagement
**Type**: `BrowserSetting`
**Description**: Determines various settings for color management.
**Properties**:
- `mode` - Color management mode
- `useNativeSRGB` - Whether to use native sRGB
- `useWebRenderCompositor` - Whether to use WebRender compositor

### contextMenuShowEvent
**Type**: `BrowserSetting`
**Description**: Determines the mouse event that triggers a context menu popup.
**Values**:
- `"mouseup"` - Show on mouse up
- `"mousedown"` - Show on mouse down

### ftpProtocolEnabled
**Type**: `BrowserSetting`
**Description**: Determines whether the FTP protocol is enabled.

### homepageOverride
**Type**: `BrowserSetting`
**Description**: Read the value of the browser's home page.

### imageAnimationBehavior
**Type**: `BrowserSetting`
**Description**: Determines how the browser treats animated images.
**Values**:
- `"normal"` - Animate images normally
- `"none"` - Don't animate images
- `"once"` - Animate images once

### newTabPageOverride
**Type**: `BrowserSetting`
**Description**: Reads the value of the browser's new tab page.

### newTabPosition
**Type**: `BrowserSetting`
**Description**: Controls the position of newly opened tabs relative to already open tabs.
**Values**:
- `"afterCurrent"` - Open new tab next to the current tab
- `"relatedAfterCurrent"` - Open new tab next to the current tab if related
- `"atEnd"` - Open new tab at the end of the tab strip

### openBookmarksInNewTabs
**Type**: `BrowserSetting`
**Description**: Determines whether bookmarks are opened in the current tab or a new tab.

### openSearchResultsInNewTabs
**Type**: `BrowserSetting`
**Description**: Determines whether search results are opened in the current tab or a new tab.

### openUrlbarResultsInNewTabs
**Type**: `BrowserSetting`
**Description**: Determines whether address bar autocomplete suggestions are opened in the current tab or a new tab.

### overrideContentColorScheme
**Type**: `BrowserSetting`
**Description**: Controls whether to override the browser theme (light or dark) when setting pages' preferred color scheme.
**Values**:
- `"auto"` - Follow the browser theme
- `"dark"` - Use dark color scheme
- `"light"` - Use light color scheme

### overrideDocumentColors
**Type**: `BrowserSetting`
**Description**: Controls whether the user-chosen colors override the page's colors.
**Values**:
- `"always"` - Always override
- `"auto"` - Override for high contrast themes only
- `"never"` - Never override

### tlsVersionRestrictionConfig
**Type**: `BrowserSetting`
**Description**: Read the highest and lowest versions of TLS supported by the browser.
**Properties**:
- `minimum` - Minimum TLS version
- `maximum` - Maximum TLS version

### useDocumentFonts
**Type**: `BrowserSetting`
**Description**: Controls whether the browser will use the fonts specified by a web page or use only built-in fonts.

### webNotificationsDisabled
**Type**: `BrowserSetting`
**Description**: Prevents websites from showing notifications using the Notification Web API.

### zoomFullPage
**Type**: `BrowserSetting`
**Description**: Controls whether zoom is applied to the entire page or to text only.

### zoomSiteSpecific
**Type**: `BrowserSetting`
**Description**: Controls whether page zoom is applied on a per-site or per-tab basis. If privacy.websites.resistFingerprinting is true, this setting has no effect and zoom is applied on a per-tab basis.

## Methods

Each property is a BrowserSetting object with these methods:

### get()
**Syntax**: `browser.browserSettings.propertyName.get(details)`

Gets the current value of the setting.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing details |
| details.incognito | boolean | No | false | Whether to return the setting for private browsing |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object containing:
  - `value` - The current value of the setting
  - `levelOfControl` - The level of control ("not_controllable", "controlled_by_other_extensions", "controllable_by_this_extension", or "controlled_by_this_extension")

### set()
**Syntax**: `browser.browserSettings.propertyName.set(details)`

Sets the value of the setting.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing the value to set |
| details.value | any | Yes | - | The new value for the setting |
| details.scope | string | No | "regular" | The scope ("regular", "regular_only", "incognito_persistent", or "incognito_session_only") |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the setting was successfully changed

### clear()
**Syntax**: `browser.browserSettings.propertyName.clear(details)`

Clears any modification made by the extension to this setting.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object containing details |
| details.scope | string | No | "regular" | The scope to clear |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: True if the setting was successfully cleared

## Code Examples
No code examples in source documentation

## Related APIs
- `types.BrowserSetting` - The BrowserSetting type used by this API
- `privacy` - Similar API for privacy-related settings