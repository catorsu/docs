# Firefox WebExtensions API Documentation

This directory contains comprehensive documentation for Firefox WebExtensions APIs, extracted and organized from Mozilla Developer Network (MDN) resources.

## API Index

### A
- [action](./WebExtensions/action.md) - Control browser toolbar buttons (Manifest V3+)
- [alarms](./WebExtensions/alarms.md) - Schedule code to run at specific times

### B
- [bookmarks](./WebExtensions/bookmarks.md) - Interact with the browser's bookmarking system
- [browserAction](./WebExtensions/browseraction.md) - Control browser toolbar buttons (Manifest V2, deprecated)
- [browserSettings](./WebExtensions/browsersettings.md) - Modify global browser settings
- [browsingData](./WebExtensions/browsingdata.md) - Clear browsing data

### C
- [captivePortal](./WebExtensions/captiveportal.md) - Detect captive portal state
- [clipboard](./WebExtensions/clipboard.md) - Copy images to the system clipboard
- [commands](./WebExtensions/commands.md) - Define keyboard shortcuts
- [contentScripts](./WebExtensions/contentscripts.md) - Register content scripts dynamically
- [contextualIdentities](./WebExtensions/contextualidentities.md) - Manage container tabs
- [cookies](./WebExtensions/cookies.md) - Get, set, and monitor cookies

### D
- [declarativeNetRequest](./WebExtensions/declarativenetrequest.md) - Declaratively handle network requests
- [devtools](./WebExtensions/devtools.md) - Extend Developer Tools
- [dns](./WebExtensions/dns.md) - Resolve domain names
- [dom](./WebExtensions/dom.md) - Access extension-only DOM features
- [downloads](./WebExtensions/downloads.md) - Interact with the download manager

### E
- [events](./WebExtensions/events.md) - Common types for event handling
- [extension](./WebExtensions/extension.md) - Extension utilities (mostly deprecated)
- [extensionTypes](./WebExtensions/extensiontypes.md) - Common types used across APIs

### F
- [find](./WebExtensions/find.md) - Find and highlight text in web pages

### H
- [history](./WebExtensions/history.md) - Interact with the browser history

### I
- [i18n](./WebExtensions/i18n.md) - Internationalize your extension
- [identity](./WebExtensions/identity.md) - OAuth2 authentication flows
- [idle](./WebExtensions/idle.md) - Detect when user's system is idle

### M
- [management](./WebExtensions/management.md) - Get information about installed add-ons
- [menus](./WebExtensions/menus.md) - Create context menu items

### N
- [notifications](./WebExtensions/notifications.md) - Display notifications to users

### O
- [omnibox](./WebExtensions/omnibox.md) - Register keyword for address bar

### P
- [pageAction](./WebExtensions/pageaction.md) - Control address bar buttons (Manifest V2, deprecated)
- [permissions](./WebExtensions/permissions.md) - Request additional permissions at runtime
- [pkcs11](./WebExtensions/pkcs11.md) - Access PKCS #11 security modules
- [privacy](./WebExtensions/privacy.md) - Access and modify privacy-related browser settings
- [proxy](./WebExtensions/proxy.md) - Proxy web requests

### R
- [runtime](./WebExtensions/runtime.md) - Extension information and messaging APIs

### S
- [scripting](./WebExtensions/scripting.md) - Insert JavaScript and CSS into websites
- [search](./WebExtensions/search.md) - Retrieve installed search engines and execute searches
- [sessions](./WebExtensions/sessions.md) - List and restore closed tabs and windows
- [sidebarAction](./WebExtensions/sidebaraction.md) - Control extension sidebars
- [storage](./WebExtensions/storage.md) - Store and retrieve extension data

### T
- [tabGroups](./WebExtensions/tabgroups.md) - Modify and rearrange tab groups
- [tabs](./WebExtensions/tabs.md) - Interact with browser tabs
- [theme](./WebExtensions/theme.md) - Get and update browser themes
- [topSites](./WebExtensions/topsites.md) - Access user's most visited sites
- [types](./WebExtensions/types.md) - Define BrowserSetting type for browser configuration

### U
- [userScripts](./WebExtensions/userscripts.md) - Register user scripts for webpage manipulation (Manifest V3)
- [userScripts_legacy](./WebExtensions/userscripts_legacy.md) - Register user scripts for webpage manipulation (Manifest V2)

### W
- [webNavigation](./WebExtensions/webnavigation.md) - Monitor navigation events across browser frames
- [webRequest](./WebExtensions/webrequest.md) - Monitor and modify HTTP requests and responses
- [windows](./WebExtensions/windows.md) - Create, modify, and monitor browser windows

## Overview

These APIs enable Firefox extensions to:
- Interact with browser UI elements (toolbars, menus, sidebars)
- Manage browser data (bookmarks, cookies, history, downloads)
- Monitor and modify network requests
- Work with tabs and windows
- Access browser settings and features
- Integrate with Developer Tools
- Handle user input (keyboard shortcuts, context menus)

## Manifest Versions

Most APIs work with both Manifest V2 and V3, but some differences exist:
- **Manifest V3 only**: `action`, `declarativeNetRequest` (enhanced), `scripting`
- **Manifest V2 only**: `browserAction`, `pageAction`, `contentScripts`
- **Deprecated**: Many methods in the `extension` API are deprecated in favor of `runtime` equivalents

## Permissions

Each API may require specific permissions in your manifest.json:
- **API permissions**: Listed in each API's documentation
- **Host permissions**: Required for APIs that access web content
- **Optional permissions**: Can be requested at runtime

## Browser Compatibility

While these docs focus on Firefox implementation, many APIs are compatible with Chrome and other Chromium-based browsers. Key differences:
- Firefox uses the `browser` namespace with Promises
- Chrome uses the `chrome` namespace with callbacks (Manifest V2)
- A polyfill is available for cross-browser compatibility

## Additional Resources

- [MDN WebExtensions Documentation](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions)
- [Extension Examples](https://github.com/mdn/webextensions-examples)
- [Browser Compatibility Data](https://github.com/mdn/browser-compat-data)

---

Last updated: June 2025