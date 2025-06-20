# Events

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/events
- **Version**: All versions

## Overview
Common types used by APIs that dispatch events. This API provides base types for event handling in WebExtensions, including the Event type that's used throughout other APIs for managing event listeners.

## Permissions
- No special permissions required

## Types
### Event
An object which allows the addition and removal of listeners for a browser event.

#### Methods
##### addListener()
**Syntax**: `event.addListener(callback)`

Registers an event listener to an event.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| callback | function | Yes | - | Function to call when the event occurs |

##### removeListener()
**Syntax**: `event.removeListener(callback)`

Deregisters an event listener from an event.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| callback | function | Yes | - | Listener to remove |

##### hasListener()
**Syntax**: `event.hasListener(callback)`

Tests registration status of a listener.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| callback | function | Yes | - | Listener to test |

###### Returns
- **Type**: `boolean`
- **Description**: True if callback is registered for the event

##### hasListeners()
**Syntax**: `event.hasListeners()`

Tests whether any listeners are registered to the event.

###### Returns
- **Type**: `boolean`
- **Description**: True if any listeners are registered

##### addRules()
**Syntax**: `event.addRules(rules)`

Registers rules to handle events.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| rules | Array<Rule> | Yes | - | Rules to register |

##### getRules()
**Syntax**: `event.getRules(ruleIdentifiers)`

Returns currently registered rules.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| ruleIdentifiers | Array<string> | No | - | IDs of rules to retrieve |

###### Returns
- **Type**: `Array<Rule>`
- **Description**: The rules registered to the event

##### removeRules()
**Syntax**: `event.removeRules(ruleIdentifiers)`

Unregisters currently registered rules.

###### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| ruleIdentifiers | Array<string> | No | - | IDs of rules to unregister |

### Rule
Description of a declarative rule for handling events.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | string | No | - | Optional identifier |
| tags | Array<string> | No | - | Tags to help organize rules |
| conditions | Array<any> | Yes | - | List of conditions |
| actions | Array<any> | Yes | - | List of actions |
| priority | integer | No | 100 | Rule priority |

### UrlFilter
Filters URLs for various criteria. If any of the given criteria match, then the whole filter matches.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| hostContains | string | No | - | Matches if the host name contains this string |
| hostEquals | string | No | - | Matches if the host name equals this string |
| hostPrefix | string | No | - | Matches if the host name starts with this string |
| hostSuffix | string | No | - | Matches if the host name ends with this string |
| pathContains | string | No | - | Matches if the path contains this string |
| pathEquals | string | No | - | Matches if the path equals this string |
| pathPrefix | string | No | - | Matches if the path starts with this string |
| pathSuffix | string | No | - | Matches if the path ends with this string |
| queryContains | string | No | - | Matches if the query contains this string |
| queryEquals | string | No | - | Matches if the query equals this string |
| queryPrefix | string | No | - | Matches if the query starts with this string |
| querySuffix | string | No | - | Matches if the query ends with this string |
| urlContains | string | No | - | Matches if the URL contains this string |
| urlEquals | string | No | - | Matches if the URL equals this string |
| urlMatches | string | No | - | Matches if the URL matches this regular expression |
| originAndPathMatches | string | No | - | Matches origin and path against a regular expression |
| urlPrefix | string | No | - | Matches if the URL starts with this string |
| urlSuffix | string | No | - | Matches if the URL ends with this string |
| schemes | Array<string> | No | - | Matches if the scheme is in this list |
| ports | Array<integer or Array<integer>> | No | - | Matches if the port is in this list |

## Methods
None (this API only provides types)

## Events
None (this API only provides types)

## Code Examples
```javascript
// Example of using Event type methods
// (typically you work with specific events from other APIs)

// Adding a listener
browser.tabs.onCreated.addListener(function(tab) {
  console.log("New tab created:", tab.id);
});

// Checking if listener exists
if (browser.tabs.onCreated.hasListener(myListener)) {
  console.log("Listener is registered");
}

// Removing a listener
browser.tabs.onCreated.removeListener(myListener);

// Checking if any listeners exist
if (browser.tabs.onCreated.hasListeners()) {
  console.log("There are listeners for tab creation");
}
```

## Related APIs
- All WebExtension APIs that fire events use these types
- `webRequest` - For network request events
- `tabs` - For tab-related events
- `runtime` - For extension lifecycle events