# tabs

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/tabs
- **Version**: Current (as of June 2025)

## Overview

Interact with the browser's tab system. You can use this API to get a list of opened tabs, filtered by various criteria, and to open, update, move, reload, and remove tabs. You can't directly access the content hosted by tabs using this API, but you can insert JavaScript and CSS into tabs using the scripting API (Manifest V3) or tabs.executeScript()/tabs.insertCSS() APIs (Manifest V2).

## Permissions

You can use most of this API without any special permission. However:
- To access `Tab.url`, `Tab.title`, and `Tab.favIconUrl`, you need the `"tabs"` permission or host permissions that match `Tab.url`
- To use `tabs.executeScript()` or `tabs.insertCSS()`, you must have host permission for the tab
- Alternatively, you can get these permissions temporarily for the currently active tab using the `"activeTab"` permission

## Types

### Tab
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| active | boolean | Yes | - | Whether the tab is active in its window |
| attention | boolean | No | false | Whether the tab is drawing attention |
| audible | boolean | No | false | Whether the tab is producing sound |
| autoDiscardable | boolean | No | true | Whether the tab can be discarded by the browser |
| cookieStoreId | string | No | - | The cookie store ID for the tab |
| discarded | boolean | No | false | Whether the tab is discarded |
| favIconUrl | string | No | - | The URL of the tab's favicon |
| groupId | integer | No | -1 | The ID of the group the tab belongs to |
| height | integer | No | - | The height of the tab in pixels |
| hidden | boolean | No | false | Whether the tab is hidden |
| highlighted | boolean | Yes | - | Whether the tab is highlighted |
| id | integer | No | - | The ID of the tab. Tab IDs are unique within a browser session |
| incognito | boolean | Yes | - | Whether the tab is in an incognito window |
| index | integer | Yes | - | The zero-based index of the tab within its window |
| mutedInfo | MutedInfo | No | - | The muted state of the tab |
| openerTabId | integer | No | - | The ID of the tab that opened this tab |
| pinned | boolean | Yes | - | Whether the tab is pinned |
| selected | boolean | Yes | - | Whether the tab is selected (deprecated, use highlighted) |
| sessionId | string | No | - | The session ID for the tab |
| status | TabStatus | No | - | The loading status of the tab |
| title | string | No | - | The title of the tab |
| url | string | No | - | The URL the tab is displaying |
| width | integer | No | - | The width of the tab in pixels |
| windowId | integer | Yes | - | The ID of the window the tab is contained within |

### TabStatus
Indicates whether the tab has finished loading:
- `"loading"` - The tab is still loading
- `"complete"` - The tab has finished loading

### MutedInfo
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| muted | boolean | Yes | - | Whether the tab is currently muted |
| reason | MutedInfoReason | No | - | The reason the tab was muted or unmuted |
| extensionId | string | No | - | The ID of the extension that changed the muted state |

### MutedInfoReason
Specifies the reason a tab was muted or unmuted:
- `"user"` - User muted/unmuted the tab
- `"capture"` - Tab was muted due to audio capture
- `"extension"` - An extension muted/unmuted the tab

### WindowType
The type of window that hosts this tab:
- `"normal"` - Normal browser window
- `"popup"` - Browser popup window
- `"panel"` - Panel window
- `"devtools"` - Developer tools window

### ZoomSettings
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| defaultZoomFactor | number | No | - | The default zoom level for the tab |
| mode | ZoomSettingsMode | No | - | How zoom changes are handled |
| scope | ZoomSettingsScope | No | - | Whether zoom changes persist |

## Properties

### TAB_ID_NONE
**Type**: `integer`
**Value**: `-1`

A special ID value given to tabs that are not browser tabs (for example, tabs in devtools windows).

## Methods

### get()
**Syntax**: `browser.tabs.get(tabId)`

Retrieves details about the specified tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | Yes | - | The ID of the tab to get |

#### Returns
- **Type**: `Promise<Tab>`
- **Description**: A Promise that resolves to a Tab object

#### Code Examples
```javascript
browser.tabs.get(1).then((tab) => {
  console.log(`Tab title: ${tab.title}`);
  console.log(`Tab URL: ${tab.url}`);
});
```

### query()
**Syntax**: `browser.tabs.query(queryInfo)`

Gets all tabs that have the specified properties, or all tabs if no properties are specified.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| queryInfo | object | No | {} | Query criteria |
| queryInfo.active | boolean | No | - | Whether the tabs are active |
| queryInfo.audible | boolean | No | - | Whether the tabs are audible |
| queryInfo.autoDiscardable | boolean | No | - | Whether the tabs are auto-discardable |
| queryInfo.cookieStoreId | string | No | - | The cookie store ID |
| queryInfo.currentWindow | boolean | No | - | Whether the tabs are in the current window |
| queryInfo.discarded | boolean | No | - | Whether the tabs are discarded |
| queryInfo.groupId | integer | No | - | The ID of the tab group |
| queryInfo.highlighted | boolean | No | - | Whether the tabs are highlighted |
| queryInfo.index | integer | No | - | The position of tabs within their windows |
| queryInfo.muted | boolean | No | - | Whether the tabs are muted |
| queryInfo.pinned | boolean | No | - | Whether the tabs are pinned |
| queryInfo.status | TabStatus | No | - | The loading status of the tabs |
| queryInfo.title | string | No | - | Match page titles against a pattern |
| queryInfo.url | string or string[] | No | - | Match tabs against URL patterns |
| queryInfo.windowId | integer | No | - | The ID of the parent window |
| queryInfo.windowType | WindowType | No | - | The type of window |

#### Returns
- **Type**: `Promise<Tab[]>`
- **Description**: A Promise that resolves to an array of Tab objects

#### Code Examples
```javascript
// Get all tabs
browser.tabs.query({}).then((tabs) => {
  console.log(`Found ${tabs.length} tabs`);
});

// Get active tab in current window
browser.tabs.query({active: true, currentWindow: true}).then((tabs) => {
  console.log(`Active tab: ${tabs[0].title}`);
});

// Get pinned tabs
browser.tabs.query({pinned: true}).then((tabs) => {
  console.log(`Found ${tabs.length} pinned tabs`);
});
```

### create()
**Syntax**: `browser.tabs.create(createProperties)`

Creates a new tab.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| createProperties | object | No | {} | Properties for the new tab |
| createProperties.active | boolean | No | true | Whether the tab should become the active tab |
| createProperties.cookieStoreId | string | No | - | The cookie store ID for the new tab |
| createProperties.index | integer | No | - | The position where the tab should be inserted |
| createProperties.openerTabId | integer | No | - | The ID of the tab that opened this tab |
| createProperties.pinned | boolean | No | false | Whether the tab should be pinned |
| createProperties.url | string | No | - | The URL to navigate the tab to initially |
| createProperties.windowId | integer | No | - | The window to create the new tab in |

#### Returns
- **Type**: `Promise<Tab>`
- **Description**: A Promise that resolves to the created Tab object

#### Code Examples
```javascript
// Create new tab with URL
browser.tabs.create({
  url: "https://example.com"
});

// Create pinned tab in specific position
browser.tabs.create({
  url: "https://example.com",
  pinned: true,
  index: 0
});
```

### update()
**Syntax**: `browser.tabs.update(tabId, updateProperties)`

Modifies the properties of a tab. Properties that are not specified in updateProperties are not modified.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | No | - | The ID of the tab to update. Defaults to active tab |
| updateProperties | object | Yes | - | Properties to update |
| updateProperties.active | boolean | No | - | Whether the tab should be active |
| updateProperties.autoDiscardable | boolean | No | - | Whether the tab should be auto-discardable |
| updateProperties.highlighted | boolean | No | - | Whether the tab should be highlighted |
| updateProperties.muted | boolean | No | - | Whether the tab should be muted |
| updateProperties.openerTabId | integer | No | - | The ID of the tab that opened this tab |
| updateProperties.pinned | boolean | No | - | Whether the tab should be pinned |
| updateProperties.url | string | No | - | A URL to navigate the tab to |

#### Returns
- **Type**: `Promise<Tab>`
- **Description**: A Promise that resolves to the updated Tab object

#### Code Examples
```javascript
// Navigate tab to new URL
browser.tabs.update(1, {url: "https://example.com"});

// Pin the current tab
browser.tabs.update({pinned: true});

// Mute a tab
browser.tabs.update(1, {muted: true});
```

### remove()
**Syntax**: `browser.tabs.remove(tabIds)`

Closes one or more tabs.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabIds | integer or integer[] | Yes | - | The tab ID or array of tab IDs to close |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the tabs are closed

#### Code Examples
```javascript
// Close single tab
browser.tabs.remove(1);

// Close multiple tabs
browser.tabs.remove([1, 2, 3]);
```

### move()
**Syntax**: `browser.tabs.move(tabIds, moveProperties)`

Moves one or more tabs to a new position within the same window, or to a new window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabIds | integer or integer[] | Yes | - | The tab ID or array of tab IDs to move |
| moveProperties | object | Yes | - | Properties specifying how to move the tabs |
| moveProperties.index | integer | Yes | - | The position to move the tabs to |
| moveProperties.windowId | integer | No | - | The window to move the tabs to |

#### Returns
- **Type**: `Promise<Tab or Tab[]>`
- **Description**: A Promise that resolves to the moved Tab(s)

#### Code Examples
```javascript
// Move tab to position 0
browser.tabs.move(1, {index: 0});

// Move tab to different window
browser.tabs.move(1, {windowId: 2, index: 0});
```

### reload()
**Syntax**: `browser.tabs.reload(tabId, reloadProperties)`

Reload a tab, optionally bypassing the local web cache.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabId | integer | No | - | The ID of the tab to reload. Defaults to active tab |
| reloadProperties | object | No | {} | Reload options |
| reloadProperties.bypassCache | boolean | No | false | Whether to bypass the local web cache |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the reload begins

#### Code Examples
```javascript
// Reload current tab
browser.tabs.reload();

// Reload tab bypassing cache
browser.tabs.reload(1, {bypassCache: true});
```

### group()
**Syntax**: `browser.tabs.group(options)`

Adds tabs to a tab group.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Group options |
| options.createProperties | object | No | - | Properties for creating a new group |
| options.groupId | integer | No | - | ID of existing group to add tabs to |
| options.tabIds | integer or integer[] | Yes | - | Tab IDs to add to the group |

#### Returns
- **Type**: `Promise<integer>`
- **Description**: A Promise that resolves to the group ID

#### Code Examples
```javascript
// Create new group with tabs
browser.tabs.group({
  tabIds: [1, 2, 3],
  createProperties: {
    title: "Work Tabs"
  }
});

// Add tabs to existing group
browser.tabs.group({
  tabIds: [4, 5],
  groupId: 1
});
```

### ungroup()
**Syntax**: `browser.tabs.ungroup(tabIds)`

Removes tabs from tab groups.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| tabIds | integer or integer[] | Yes | - | Tab IDs to remove from groups |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when tabs are ungrouped

#### Code Examples
```javascript
// Ungroup single tab
browser.tabs.ungroup(1);

// Ungroup multiple tabs
browser.tabs.ungroup([1, 2, 3]);
```

## Events

### onCreated
**Fired when**: A tab is created

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| tab | Tab | The created tab |

#### Code Examples
```javascript
browser.tabs.onCreated.addListener((tab) => {
  console.log(`New tab created: ${tab.title}`);
});
```

### onUpdated
**Fired when**: A tab is updated

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| tabId | integer | The ID of the updated tab |
| changeInfo | object | Properties that changed |
| tab | Tab | The updated tab |

#### Code Examples
```javascript
browser.tabs.onUpdated.addListener((tabId, changeInfo, tab) => {
  if (changeInfo.status === "complete") {
    console.log(`Tab ${tabId} finished loading: ${tab.title}`);
  }
});
```

### onRemoved
**Fired when**: A tab is closed

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| tabId | integer | The ID of the removed tab |
| removeInfo | object | Information about the removal |

#### Code Examples
```javascript
browser.tabs.onRemoved.addListener((tabId, removeInfo) => {
  console.log(`Tab ${tabId} was closed`);
});
```

### onActivated
**Fired when**: The active tab in a window changes

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| activeInfo | object | Information about the activation |
| activeInfo.tabId | integer | The ID of the newly active tab |
| activeInfo.windowId | integer | The ID of the window |

#### Code Examples
```javascript
browser.tabs.onActivated.addListener((activeInfo) => {
  console.log(`Tab ${activeInfo.tabId} became active`);
});
```

## Related APIs
- `tabGroups` - For managing tab groups
- `windows` - For window management
- `scripting` - For injecting scripts into tabs (Manifest V3)
- `sessions` - For restoring closed tabs
