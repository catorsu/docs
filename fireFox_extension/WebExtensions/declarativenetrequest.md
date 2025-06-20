# DeclarativeNetRequest

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/declarativeNetRequest
- **Version**: Firefox 113+, Chrome 84+

## Overview
This API enables extensions to specify conditions and actions that describe how network requests should be handled. These declarative rules enable the browser to evaluate and modify network requests without notifying extensions about individual network requests.

The API uses declarative rules organized into rulesets (static, dynamic, and session) to efficiently process network requests in the browser without requiring JavaScript evaluation for each request.

## Permissions
- `declarativeNetRequest` - Allows blocking and upgrading requests without host permissions
- `declarativeNetRequestWithHostAccess` - Requires host permissions for blocking/upgrading
- `declarativeNetRequestFeedback` - Required for debugging methods
- Host permissions - Required for redirecting requests or modifying headers

## Types
### Rule
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | integer | Yes | - | Unique identifier within a ruleset (must be >= 1) |
| priority | integer | No | 1 | Rule priority (must be >= 1) |
| condition | RuleCondition | Yes | - | The condition under which this rule is triggered |
| action | RuleAction | Yes | - | The action to take when the rule is matched |

### RuleCondition
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| urlFilter | string | No* | - | Pattern to match against the request URL |
| regexFilter | string | No* | - | Regular expression to match against the request URL |
| isUrlFilterCaseSensitive | boolean | No | false | Whether urlFilter is case sensitive |
| initiatorDomains | Array<string> | No | - | The request initiator domains |
| excludedInitiatorDomains | Array<string> | No | - | Excluded initiator domains |
| requestDomains | Array<string> | No | - | The request domains |
| excludedRequestDomains | Array<string> | No | - | Excluded request domains |
| resourceTypes | Array<ResourceType> | No | All types | List of resource types to match |
| excludedResourceTypes | Array<ResourceType> | No | - | Excluded resource types |
| requestMethods | Array<string> | No | All methods | HTTP request methods to match |
| excludedRequestMethods | Array<string> | No | - | Excluded HTTP methods |
| tabIds | Array<integer> | No | - | List of tab IDs to match |
| excludedTabIds | Array<integer> | No | - | Excluded tab IDs |

*Note: Either urlFilter or regexFilter must be specified

### RuleAction
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| type | string | Yes | - | The type of action ("block", "redirect", "allow", "upgradeScheme", "modifyHeaders", "allowAllRequests") |
| redirect | Redirect | No* | - | How the redirect should be performed |
| requestHeaders | Array<ModifyHeaderInfo> | No* | - | Request headers to modify |
| responseHeaders | Array<ModifyHeaderInfo> | No* | - | Response headers to modify |

*Required for specific action types

### ResourceType
| Value | Description |
|-------|-------------|
| "main_frame" | Top-level document |
| "sub_frame" | Document inside a frame |
| "stylesheet" | CSS stylesheet |
| "script" | JavaScript file |
| "image" | Image |
| "font" | Font file |
| "object" | Plugin object |
| "xmlhttprequest" | XMLHttpRequest |
| "ping" | Ping request |
| "csp_report" | CSP report |
| "media" | Audio/video |
| "websocket" | WebSocket connection |
| "webtransport" | WebTransport connection |
| "webbundle" | Web Bundle |
| "other" | Other resource types |

### Redirect
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| url | string | No* | - | The redirect URL |
| extensionPath | string | No* | - | Path relative to extension directory |
| transform | URLTransform | No* | - | URL transformations to perform |
| regexSubstitution | string | No* | - | Substitution pattern for regex matches |

*One of these must be specified

### ModifyHeaderInfo
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| header | string | Yes | - | The name of the header |
| operation | string | Yes | - | The operation ("append", "set", "remove") |
| value | string | No* | - | The new header value |

*Required for "append" and "set" operations

### MatchedRule
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| ruleId | integer | Yes | - | The ID of the matched rule |
| rulesetId | string | Yes | - | The ID of the ruleset |
| extensionId | string | No | - | The ID of the extension |
| rule | Rule | Yes | - | The matched rule |

## Properties
### Constants
- `DYNAMIC_RULESET_ID` - "dynamic" (ID for dynamic rules)
- `SESSION_RULESET_ID` - "session" (ID for session rules)
- `GUARANTEED_MINIMUM_STATIC_RULES` - 30,000
- `MAX_NUMBER_OF_STATIC_RULESETS` - 100
- `MAX_NUMBER_OF_ENABLED_STATIC_RULESETS` - 20
- `MAX_NUMBER_OF_DISABLED_STATIC_RULES` - 5,000
- `MAX_NUMBER_OF_DYNAMIC_RULES` - 30,000
- `MAX_NUMBER_OF_SESSION_RULES` - 30,000
- `MAX_NUMBER_OF_REGEX_RULES` - 1,000
- `GETMATCHEDRULES_QUOTA_INTERVAL` - 10 minutes
- `MAX_GETMATCHEDRULES_CALLS_PER_INTERVAL` - 20

## Methods
### getAvailableStaticRuleCount()
**Syntax**: `browser.declarativeNetRequest.getAvailableStaticRuleCount()`

Returns the number of static rules an extension can enable before the global limit is reached.

#### Returns
- **Type**: `Promise<number>`
- **Description**: The number of rules that can be enabled

### getDynamicRules()
**Syntax**: `browser.declarativeNetRequest.getDynamicRules(filter)`

Returns the set of dynamic rules for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | object | No | {} | Filter for specific rule IDs |
| filter.ruleIds | Array<integer> | No | - | Rule IDs to retrieve |

#### Returns
- **Type**: `Promise<Array<Rule>>`
- **Description**: The dynamic rules

### getSessionRules()
**Syntax**: `browser.declarativeNetRequest.getSessionRules(filter)`

Returns the set of session-scoped rules for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | object | No | {} | Filter for specific rule IDs |
| filter.ruleIds | Array<integer> | No | - | Rule IDs to retrieve |

#### Returns
- **Type**: `Promise<Array<Rule>>`
- **Description**: The session rules

### updateDynamicRules()
**Syntax**: `browser.declarativeNetRequest.updateDynamicRules(options)`

Modifies the active set of dynamic rules for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Update options |
| options.addRules | Array<Rule> | No | - | Rules to add |
| options.removeRuleIds | Array<integer> | No | - | IDs of rules to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when rules are updated

### updateSessionRules()
**Syntax**: `browser.declarativeNetRequest.updateSessionRules(options)`

Modifies the set of session-scoped rules for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Update options |
| options.addRules | Array<Rule> | No | - | Rules to add |
| options.removeRuleIds | Array<integer> | No | - | IDs of rules to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when rules are updated

### updateEnabledRulesets()
**Syntax**: `browser.declarativeNetRequest.updateEnabledRulesets(options)`

Updates the set of active static rulesets for the extension.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Update options |
| options.enableRulesetIds | Array<string> | No | - | Ruleset IDs to enable |
| options.disableRulesetIds | Array<string> | No | - | Ruleset IDs to disable |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when rulesets are updated

### getEnabledRulesets()
**Syntax**: `browser.declarativeNetRequest.getEnabledRulesets()`

Returns the IDs for the set of enabled static rulesets.

#### Returns
- **Type**: `Promise<Array<string>>`
- **Description**: Array of enabled ruleset IDs

### testMatchOutcome()
**Syntax**: `browser.declarativeNetRequest.testMatchOutcome(request, options)`

Checks if any rules would match a hypothetical request. Requires "declarativeNetRequestFeedback" permission.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| request | object | Yes | - | The hypothetical request to test |
| options | object | No | - | Options for the test |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with matchedRules array

### getMatchedRules()
**Syntax**: `browser.declarativeNetRequest.getMatchedRules(filter)`

Returns all rules matched. Requires "declarativeNetRequestFeedback" permission.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| filter | object | No | - | Filter for matched rules |
| filter.tabId | integer | No | - | Tab to get matched rules for |
| filter.minTimeStamp | number | No | - | Minimum timestamp |
| filter.maxTimeStamp | number | No | - | Maximum timestamp |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with rulesMatchedInfo array

### isRegexSupported()
**Syntax**: `browser.declarativeNetRequest.isRegexSupported(regexOptions)`

Checks if a regular expression is supported.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| regexOptions | object | Yes | - | The regex to test |
| regexOptions.regex | string | Yes | - | The regular expression |
| regexOptions.isCaseSensitive | boolean | No | false | Whether the regex is case sensitive |
| regexOptions.requireCapturing | boolean | No | false | Whether capturing groups are required |

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with isSupported boolean and reason string

### setExtensionActionOptions()
**Syntax**: `browser.declarativeNetRequest.setExtensionActionOptions(options)`

Configures how the action count for tabs is handled.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Configuration options |
| options.displayActionCountAsBadgeText | boolean | No | - | Whether to display count as badge text |
| options.tabUpdate | object | No | - | Details of how tab counts are calculated |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when options are set

## Events
### onRuleMatchedDebug
**Fired when**: A rule is matched with a request (requires "declarativeNetRequestFeedback" permission)

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| info | object | Information about the matched rule |
| info.rule | MatchedRule | The matched rule |
| info.request | object | Details about the request |

## Code Examples
```json
// In manifest.json
{
  "permissions": ["declarativeNetRequest"],
  "declarative_net_request": {
    "rule_resources": [{
      "id": "ruleset_1",
      "enabled": true,
      "path": "rules_1.json"
    }]
  }
}
```

```json
// In rules_1.json
[
  {
    "id": 1,
    "priority": 1,
    "action": { "type": "block" },
    "condition": {
      "urlFilter": "||example.com/ads/*",
      "resourceTypes": ["script", "image"]
    }
  }
]
```

## Related APIs
- `webRequest` - The event-based API for intercepting requests
- `webNavigation` - For monitoring navigation events