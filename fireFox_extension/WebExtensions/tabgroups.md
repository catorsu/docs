# tabGroups

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/tabGroups
- **Version**: Current (as of June 2025)

## Overview

This API enables extensions to modify and rearrange tab groups. Tab groups are a browser feature that allows users to organize related tabs together with custom names and colors for better organization and workflow management.

Tab groups may persist across browser restarts as part of session restore. However, tab groups in private browsing windows do not persist across restarts. When a tab group is restored, its `groupId` may differ from its original value.

The tabGroups API doesn't offer the ability to create or remove tab groups. Use the `tabs.group()` and `tabs.ungroup()` methods instead. To query the position of a tab group within a window, use `tabs.query()`. These APIs in the tabs namespace don't require any permissions.

## Permissions

To use this API, an extension must request the `"tabGroups"` permission in its manifest.json file:

```json
{
  "permissions": ["tabGroups"]
}
```

The "tabGroups" permission is not shown to users in permission prompts.

## Types

### Color
The color of a tab group. Values include:
- `"grey"`
- `"blue"`
- `"red"`
- `"yellow"`
- `"green"`
- `"pink"`
- `"purple"`
- `"cyan"`
- `"orange"`

### TabGroup
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| collapsed | boolean | Yes | - | Whether the group is collapsed. A collapsed group is one whose tabs are hidden |
| color | Color | Yes | - | The color of the group |
| id | integer | Yes | - | The ID of the group. Group IDs are unique within a browser session |
| title | string | No | "" | The title of the group |
| windowId | integer | Yes | - | The ID of the window that contains the group |

## Properties

### TAB_GROUP_ID_NONE
**Type**: `integer`
**Value**: `-1`

The tab group ID value returned when a tab isn't in a tab group.

## Methods

### get()
**Syntax**: `browser.tabGroups.get(groupId)`

Returns details about a tab group.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| groupId | integer | Yes | - | The ID of the group to retrieve |

#### Returns
- **Type**: `Promise<TabGroup>`
- **Description**: A Promise that resolves to a TabGroup object containing details about the group

#### Code Examples
```javascript
browser.tabGroups.get(1).then((group) => {
  console.log(`Group: ${group.title}, Color: ${group.color}`);
});
```

### move()
**Syntax**: `browser.tabGroups.move(groupId, moveProperties)`

Moves a tab group within or to another window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| groupId | integer | Yes | - | The ID of the group to move |
| moveProperties | object | Yes | - | Properties specifying how to move the group |
| moveProperties.index | integer | Yes | - | The position to move the group to |
| moveProperties.windowId | integer | No | - | The window to move the group to |

#### Returns
- **Type**: `Promise<TabGroup>`
- **Description**: A Promise that resolves to the moved TabGroup object

#### Code Examples
```javascript
// Move group to position 2 in same window
browser.tabGroups.move(1, {index: 2});

// Move group to different window
browser.tabGroups.move(1, {
  windowId: 2,
  index: 0
});
```

### query()
**Syntax**: `browser.tabGroups.query(queryInfo)`

Returns all tab groups or finds tab groups with certain properties.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| queryInfo | object | No | {} | Properties to match against |
| queryInfo.collapsed | boolean | No | - | Whether the groups are collapsed |
| queryInfo.color | Color | No | - | The color of the groups |
| queryInfo.title | string | No | - | Match group titles against a pattern |
| queryInfo.windowId | integer | No | - | The ID of the parent window |

#### Returns
- **Type**: `Promise<TabGroup[]>`
- **Description**: A Promise that resolves to an array of TabGroup objects

#### Code Examples
```javascript
// Get all tab groups
browser.tabGroups.query({}).then((groups) => {
  groups.forEach(group => {
    console.log(`Group: ${group.title}, Color: ${group.color}`);
  });
});

// Get collapsed groups
browser.tabGroups.query({collapsed: true}).then((groups) => {
  console.log(`Found ${groups.length} collapsed groups`);
});

// Get groups by color
browser.tabGroups.query({color: "blue"}).then((groups) => {
  console.log(`Found ${groups.length} blue groups`);
});
```

### update()
**Syntax**: `browser.tabGroups.update(groupId, updateProperties)`

Modifies the state of a tab group. Properties that are not specified in updateProperties are not modified.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| groupId | integer | Yes | - | The ID of the group to update |
| updateProperties | object | Yes | - | Properties to update |
| updateProperties.collapsed | boolean | No | - | Whether the group should be collapsed |
| updateProperties.color | Color | No | - | The color of the group |
| updateProperties.title | string | No | - | The title of the group |

#### Returns
- **Type**: `Promise<TabGroup>`
- **Description**: A Promise that resolves to the updated TabGroup object

#### Code Examples
```javascript
// Update group title and color
browser.tabGroups.update(1, {
  title: "Work Tabs",
  color: "blue"
});

// Collapse a group
browser.tabGroups.update(1, {collapsed: true});

// Expand a group and change color
browser.tabGroups.update(1, {
  collapsed: false,
  color: "green"
});
```

## Events

### onCreated
**Fired when**: A tab group is created

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| group | TabGroup | The created group |

#### Code Examples
```javascript
browser.tabGroups.onCreated.addListener((group) => {
  console.log(`New group created: ${group.title}`);
});
```

### onMoved
**Fired when**: A tab group is moved within a window or to another window

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| group | TabGroup | The moved group |

#### Code Examples
```javascript
browser.tabGroups.onMoved.addListener((group) => {
  console.log(`Group ${group.title} moved to window ${group.windowId}`);
});
```

### onRemoved
**Fired when**: A tab group is removed

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| group | TabGroup | The removed group |

#### Code Examples
```javascript
browser.tabGroups.onRemoved.addListener((group) => {
  console.log(`Group ${group.title} was removed`);
});
```

### onUpdated
**Fired when**: A tab group is updated

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| group | TabGroup | The updated group |

#### Code Examples
```javascript
browser.tabGroups.onUpdated.addListener((group) => {
  console.log(`Group ${group.title} was updated`);
});
```

## Related APIs
- `tabs.group()` - Add tabs to a tab group
- `tabs.ungroup()` - Remove tabs from tab groups  
- `tabs.query()` - Query tabs by group ID
- `windows` - For window management when moving groups between windows
