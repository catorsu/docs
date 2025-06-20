# sessions

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/sessions
- **Version**: Current as of June 2025

## Overview

Use the sessions API to list, and restore, tabs and windows that have been closed while the browser has been running. This API also enables extensions to store additional state associated with tabs or windows that can be retrieved when they are restored.

The API provides functions to restore closed tabs/windows and to store/retrieve custom data associated with tabs and windows.

## Permissions
- `sessions` - required to use this API

## Types

### Session
Represents a tab or window that the user has closed in the current browsing session:
- **lastModified**: number - Time when the window or tab was closed (milliseconds since epoch)
- **tab**: tabs.Tab - Tab object (if session represents a closed tab)
- **window**: windows.Window - Window object (if session represents a closed window)

### Filter
Enables you to restrict the number of Session objects returned:
- **maxResults**: number - Maximum number of sessions to return

## Properties

### MAX_SESSION_RESULTS
**Type**: `number`

The maximum number of sessions that will be returned by a call to getRecentlyClosed().

## Methods

### getRecentlyClosed()
**Syntax**: `browser.sessions.getRecentlyClosed(filter)`

Returns an array of Session objects, representing windows and tabs that were closed in the current browsing session.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | Filter | No | - | Optional filter to limit results |

#### Returns
- **Type**: `Promise<array>`
- **Description**: Promise that resolves to array of Session objects

#### Code Examples
```javascript
// Get all recently closed sessions
browser.sessions.getRecentlyClosed().then(sessions => {
  sessions.forEach(session => {
    if (session.tab) {
      console.log(`Closed tab: ${session.tab.title}`);
    } else if (session.window) {
      console.log(`Closed window with ${session.window.tabs.length} tabs`);
    }
  });
});

// Get only 5 most recent sessions
browser.sessions.getRecentlyClosed({maxResults: 5}).then(sessions => {
  console.log('Recent sessions:', sessions);
});
```

### restore()
**Syntax**: `browser.sessions.restore(sessionId)`

Restores a closed tab or window. Restoring also restores the tab's navigation history so back/forward buttons will work.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| sessionId | string | No | - | Session ID to restore (restores most recent if omitted) |

#### Returns
- **Type**: `Promise<Session>`
- **Description**: Promise that resolves to the restored Session object

#### Code Examples
```javascript
// Restore most recently closed session
browser.sessions.restore();

// Restore specific session
browser.sessions.getRecentlyClosed().then(sessions => {
  if (sessions.length > 0) {
    browser.sessions.restore(sessions[0].tab.sessionId);
  }
});
```

### setTabValue()
**Syntax**: `browser.sessions.setTabValue(tabId, key, value)`

Store a key/value pair associated with a given tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | number | Yes | - | ID of the tab |
| key | string | Yes | - | Key for the stored value |
| value | string\|object | Yes | - | Value to store |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when value is stored

#### Code Examples
```javascript
browser.sessions.setTabValue(123, "groupId", "work-tabs");
```

### getTabValue()
**Syntax**: `browser.sessions.getTabValue(tabId, key)`

Retrieve a previously stored value for a given tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | number | Yes | - | ID of the tab |
| key | string | Yes | - | Key for the stored value |

#### Returns
- **Type**: `Promise<any>`
- **Description**: Promise that resolves to the stored value

#### Code Examples
```javascript
browser.sessions.getTabValue(123, "groupId").then(groupId => {
  console.log("Tab group:", groupId);
});
```

### removeTabValue()
**Syntax**: `browser.sessions.removeTabValue(tabId, key)`

Remove a key/value pair from a given tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | number | Yes | - | ID of the tab |
| key | string | Yes | - | Key to remove |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when value is removed

### setWindowValue()
**Syntax**: `browser.sessions.setWindowValue(windowId, key, value)`

Store a key/value pair associated with a given window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | number | Yes | - | ID of the window |
| key | string | Yes | - | Key for the stored value |
| value | string\|object | Yes | - | Value to store |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when value is stored

### getWindowValue()
**Syntax**: `browser.sessions.getWindowValue(windowId, key)`

Retrieve a previously stored value for a given window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | number | Yes | - | ID of the window |
| key | string | Yes | - | Key for the stored value |

#### Returns
- **Type**: `Promise<any>`
- **Description**: Promise that resolves to the stored value

### removeWindowValue()
**Syntax**: `browser.sessions.removeWindowValue(windowId, key)`

Remove a key/value pair from a given window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | number | Yes | - | ID of the window |
| key | string | Yes | - | Key to remove |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when value is removed

### forgetClosedTab()
**Syntax**: `browser.sessions.forgetClosedTab(windowId, sessionId)`

Removes a closed tab from the browser's list of recently closed tabs.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | number | Yes | - | ID of the window that contained the tab |
| sessionId | string | Yes | - | Session ID of the closed tab |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when tab is forgotten

### forgetClosedWindow()
**Syntax**: `browser.sessions.forgetClosedWindow(sessionId)`

Removes a closed window from the browser's list of recently closed windows.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| sessionId | string | Yes | - | Session ID of the closed window |

#### Returns
- **Type**: `Promise<undefined>`
- **Description**: Promise that resolves when window is forgotten

## Events

### onChanged
**Fired when**: A tab or window is closed.

This event notifies when the list of closed tabs/windows has changed.

#### Code Examples
```javascript
browser.sessions.onChanged.addListener(() => {
  console.log("Session list changed");
  // Refresh UI showing recently closed items
});
```

## Related APIs
- `tabs` - For working with individual tabs
- `windows` - For working with browser windows
- `history` - For accessing browsing history
- `storage` - For alternative data persistence
