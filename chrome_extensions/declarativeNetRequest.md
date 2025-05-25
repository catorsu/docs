---
title: chrome.declarativeNetRequest
url: https://developer.chrome.com/docs/extensions/reference/api/declarativeNetRequest
---

## Description

The `chrome.declarativeNetRequest` API is used to block or modify network requests by specifying declarative rules. This lets extensions modify network requests without intercepting them and viewing their content, thus providing more privacy.

## Permissions

`declarativeNetRequest` `declarativeNetRequestWithHostAccess`

The `"declarativeNetRequest"` and `"declarativeNetRequestWithHostAccess"` permissions provide the same capabilities. The differences between them is when permissions are requested or granted.

`"declarativeNetRequest"`
:   Triggers a permission warning at install time but provides implicit access to `allow`, `allowAllRequests` and `block` rules. Use this when possible to avoid needing to request full access to hosts.

`"declarativeNetRequestFeedback"`
:   Enables debugging features for unpacked extensions, specifically `getMatchedRules()` and `onRuleMatchedDebug`.

`"declarativeNetRequestWithHostAccess"`
:   A permission warning is not shown at install time, but you must request host permissions before you can perform any action on a host. This is appropriate when you want to use declarative net request rules in an extension which already has host permissions without generating additional warnings.

## Availability

Chrome 84+

## Manifest

In addition to the permissions described previously, certain types of rulesets, static rulesets specifically, require declaring the `"declarative_net_request"` manifest key, which should be a dictionary with a single key called `"rule_resources"`. This key is an array containing dictionaries of type `Ruleset`, as shown in the following. (Note that the name '`Ruleset`' does not appear in the manifest's JSON since it is merely an array.) Static rulesets are explained later in this document.

```json
{
  "name": "My extension",
  ...
  "declarative_net_request" : {
    "rule_resources" : [
      {
        "id": "ruleset_1",
        "enabled": true,
        "path": "rules_1.json"
      },
      {
        "id": "ruleset_2",
        "enabled": false,
        "path": "rules_2.json"
      }
    ]
  },
  "permissions": [
    "declarativeNetRequest",
    "declarativeNetRequestFeedback"
  ],
  "host_permissions": [
    "http://www.blogger.com/*",
    "http://*.google.com/*"
  ],
  ...
}
```

## Rules and rulesets

To use this API, specify one or more rulesets. A ruleset contains an array of rules. A single rule does one of the following:

*   Block a network request.
*   Upgrade the schema (http to https).
*   Prevent a request from getting blocked by negating any matching blocked rules.
*   Redirect a network request.
*   Modify request or response headers.

There are three types of rulesets, managed in slightly different ways.

`Dynamic`
:   Persist across browser sessions and extension upgrades and are managed using JavaScript while an extension is in use.

`Session`
:   Cleared when the browser shuts down and when a new version of the extension is installed. Session rules are managed using JavaScript while an extension is in use.

`Static`
:   Packaged, installed, and updated when an extension is installed or upgraded. Static rules are stored in JSON-formatted rule files and listed in the manifest file.

### Dynamic and session-scoped rulesets

Dynamic and session rulesets are managed using JavaScript while an extension is in use.

*   Dynamic rules persist across browser sessions and extension upgrades.
*   Session rules are cleared when the browser shuts down and when a new version of the extension is installed.

There is only one each of these ruleset types. An extension can add or remove rules to them dynamically by calling `updateDynamicRules()` and `updateSessionRules()`, provided the rule limits aren't exceeded. For information on rule limits, see Rule limits. You can see an example of this under code examples.

### Static rulesets

Unlike dynamic and session rules, static rules are packaged, installed, and updated when an extension is installed or upgraded. They're stored in rule files in JSON format, which are indicated to the extension using the `"declarative_net_request"` and `"rule_resources"` keys as described above, as well as one or more `Ruleset` dictionaries. A `Ruleset` dictionary contains a path to the rule file, an ID for the ruleset contained in the file, and whether the ruleset is enabled or disabled. The last two are important when you enable or disable a ruleset programmatically.

```json
{
  ...
  "declarative_net_request" : {
    "rule_resources" : [
      {
        "id": "ruleset_1",
        "enabled": true,
        "path": "rules_1.json"
      },
      ...
    ]
  }
  ...
}
```

To test rule files, load your extension unpacked. Errors and warnings about invalid static rules are only displayed for unpacked extensions. Invalid static rules in packed extensions are ignored.

## Expedited review

Changes to static rulesets may be eligible for expedited review. See expedited review for eligible changes.

## Enable and disable static rules and rulesets

Both individual static rules and complete static rulesets may be enabled or disabled at runtime.

The set of enabled static rules and rulesets is persisted across browser sessions. Neither are persisted across extension updates, meaning that only rules you chose to leave in your rule files are available after an update.

For performance reasons there are also limits to the number of rules and rulesets that may be enabled at one time. Call `getAvailableStaticRuleCount()` to check the number of additional rules that may be enabled. For information on rule limits, see Rule limits.

To enable or disable static rules, call `updateStaticRules()`. This method takes an `UpdateStaticRulesOptions` object, which contains arrays of IDs of rules to enable or disable. The IDs are defined using the `"id"` key of the `Ruleset` dictionary. There is a maximum limit of 5000 disabled static rules.

To enable or disable static rulesets, call `updateEnabledRulesets()`. This method takes an `UpdateRulesetOptions` object, which contains arrays of IDs of rulesets to enable or disable. The IDs are defined using the `"id"` key of the `Ruleset` dictionary.

## Build rules

Regardless of type, a rule starts with four fields as shown in the following. While the `"id"` and `"priority"` keys take a number, the `"action"` and `"condition"` keys may provide several blocking and redirecting conditions. The following rule blocks all script requests originating from `"foo.com"` to any URL with `"abc"` as a substring.

```json
{
  "id" : 1,
  "priority": 1,
  "action" : { "type" : "block" },
  "condition" : {
    "urlFilter" : "abc",
    "initiatorDomains" : ["foo.com"],
    "resourceTypes" : ["script"]
  }
}
```

## URL matching

Declarative Net Request provides the ability to match URLs with either a pattern matching syntax or regular expressions.

### URL filter syntax

A rule's `"condition"` key allows a `"urlFilter"` key for acting on URLs under a specified domain. You create patterns using pattern matching tokens. Here are a few examples.

| `urlFilter`         | Matches                                         | Does not match        |
| ------------------- | ----------------------------------------------- | --------------------- |
| `"abc"`             | `https://abcd.com` `https://example.com/abcd`   | `https://ab.com`      |
| `"abc*d"`           | `https://abcd.com` `https://example.com/abcxyzd`| `https://abc.com`     |
| `"||a.example.com"` | `https://a.example.com/` `https://b.a.example.com/xyz` `https://a.example.company` | `https://example.com/`|
| `"|https*"`         | `https://example.com`                           | `http://example.com/` `http://https.com` |
| `"example*^123|"`   | `https://example.com/123` `http://abc.com/example?123` | `https://example.com/1234` `https://abc.com/example0123` |

### Regular expressions

Conditions can also use regular expressions. See the `"regexFilter"` key. To learn about the limits that apply to these conditions, see Rules that use regular expressions.

### Write good URL conditions

Take care when writing rules to always match an entire domain. Otherwise, your rule may match in situations that are unexpected. For example, when using the pattern matching syntax:

*   `google.com` incorrectly matches `https://example.com/?param=google.com`
*   `||google.com` incorrectly matches `https://google.company`
*   `https://www.google.com` incorrectly matches `https://example.com/?param=https://www.google.com`

Consider using:

*   `||google.com/`, which matches all paths and all subdomains.
*   `|https://www.google.com/` which matches all paths and no subdomains.

Similarly, use the `^` and `/` characters to anchor a regular expression. For example, `^https:\/\/www\.google\.com\/` matches any path on `https://www.google.com`.

## Rule evaluation

DNR rules are applied by the browser across various stages of the network request lifecycle.

### Before the request

Before a request is made, an extension can block or redirect (including upgrading the scheme from HTTP to HTTPS) it with a matching rule.

For each extension, the browser determines a list of matching rules. Rules with a `modifyHeaders` action are not included here as they will be handled later. Additionally, rules with a `responseHeaders` condition will be considered later (when response headers are available) and are not included.

Then, for each extension, Chrome picks at most one candidate per request. Chrome finds a matching rule, by ordering all matching rules by priority. Rules with the same priority are ordered by action (`allow` or `allowAllRequests` > `block` > `upgradeScheme` > `redirect`).

If the candidate is an `allow` or `allowAllRequests` rule, or the frame the request is being made in previously matched an `allowAllRequests` rule of higher or equal priority from this extension, the request is "allowed" and the extension won't have any effect on the request.

If more than one extension wants to block or redirect this request, a single action to take is chosen. Chrome does this by sorting the rules in the order `block` > `redirect` or `upgradeScheme` > `allow` or `allowAllRequests`. If two rules are of the same type, Chrome chooses the rule from the most recently installed extension.

Caution: Browser vendors have agreed not to standardize the order in which rules with the same action and priority run. This can change between runs or browser versions, even when spread between multiple types of ruleset (such as a static rule and a session rule). When ordering is important, you should always explicitly specify a priority.

### Before request headers are sent

Before Chrome sends request headers to the server, the headers are updated based on matching `modifyHeaders` rules.

Within a single extension, Chrome builds the list of modifications to perform by finding all matching `modifyHeaders` rules. Similar to before, only rules which have a higher priority than any matching `allow` or `allowAllRequests` rules are included.

These rules are applied by Chrome in an order such that rules from a more recently installed extension are always evaluated before rules from an older extension. Additionally, rules of a higher priority from one extension are always applied before rules of a lower priority from the same extension. Notably, even across extensions:

*   If a rule appends to a header, then lower priority rules can only append to that header. `Set` and `remove` operations are not allowed.
*   If a rule sets a header, then only lower priority rules from the same extension can append to that header. No other modifications are allowed.
*   If a rule removes a header, then lower priority rules cannot further modify the header.

### Once a response is received

Once the response headers have been received, Chrome evaluates rules with a `responseHeaders` condition.

After sorting these rules by action and priority and excluding any rules made redundant by a matching `allow` or `allowAllRequests` rule (this happens identically to the steps in "Before the request"), Chrome may block or redirect the request on behalf of an extension.

Note that if a request made it to this stage, the request has already been sent to the server and the server has received data like the request body. A `block` or `redirect` rule with a response headers condition will still run–but cannot actually block or redirect the request.

In the case of a `block` rule, this is handled by the page which made the request receiving a blocked response and Chrome terminating the request early. In the case of a `redirect` rule, Chrome makes a new request to the redirected URL. Make sure to consider if these behaviors meet the privacy expectations for your extension.

If the request is not blocked or redirected, Chrome applies any `modifyHeaders` rules. Applying modifications to response headers works in the same way as described in "Before request headers are sent". Applying modifications to request headers does nothing, since the request has already been made.

## Safe rules

Safe rules are defined as rules with an action of `block`, `allow`, `allowAllRequests` or `upgradeScheme`. These rules are subject to an increased dynamic rules quota.

## Rule limits

There is a performance overhead to loading and evaluating rules in the browser, so some limits apply when using the API. Limits depend on the type of rule you're using.

### Static rules

Static rules are those specified in rule files declared in the manifest file. An extension can specify up to 100 static rulesets as part of the `"rule_resources"` manifest key, but only 50 of these rulesets can be enabled at a time. The latter is called the `MAX_NUMBER_OF_ENABLED_STATIC_RULESETS`. Collectively, those rulesets are guaranteed at least 30,000 rules. This is called the `GUARANTEED_MINIMUM_STATIC_RULES`.

Note: Prior to Chrome 120, extensions were limited to a total of 50 static rulesets, and only 10 of these could be enabled at the same time. Use the `minimum_chrome_version` manifest field to limit which Chrome versions can install your extension.

The number of rules available after that depends on how many rules are enabled by all the extensions installed on a user's browser. You can find this number at runtime by calling `getAvailableStaticRuleCount()`. You can see an example of this under code examples.

Note: Starting with Chrome 128, if a user disables an extension through `chrome://extensions`, the extension's static rules will no longer count towards the global static rule limit. This potentially frees up static rule quota for other extensions, but also means that when the extension gets re-enabled, it might have fewer static rules available than before.

### Session rules

An extension can have up to 5000 session rules. This is exposed as the `MAX_NUMBER_OF_SESSION_RULES`.

Before Chrome 120, there was a limit of 5000 combined dynamic and session rules.

### Dynamic rules

An extension can have at least 5000 dynamic rules. This is exposed as the `MAX_NUMBER_OF_UNSAFE_DYNAMIC_RULES`.

Starting in Chrome 121, there is a larger limit of 30,000 rules available for safe dynamic rules, exposed as the `MAX_NUMBER_OF_DYNAMIC_RULES`. Any unsafe rules added within the limit of 5000 will also count towards this limit.

Before Chrome 120, there was a 5000 combined dynamic and session rules limit.

### Rules that use regular expressions

All types of rules can use regular expressions; however, the total number of regular expression rules of each type cannot exceed 1000. This is called the `MAX_NUMBER_OF_REGEX_RULES`.

Additionally, each rule must be less than 2KB once compiled. This roughly correlates with the complexity of the rule. If you try to load a rule that exceeds this limit, you will see a warning like the following and the rule will be ignored.

```
rules_1.json: Rule with id 1 specified a more complex regex than allowed as part of the "regexFilter" key.
```

## Interactions with service workers

A `declarativeNetRequest` only applies to requests that reach the network stack. This includes responses from the HTTP cache, but may not include responses that go through a service worker's `onfetch` handler. `declarativeNetRequest` won't affect responses generated by the service worker or retrieved from `CacheStorage`, but it will affect calls to `fetch()` made in a service worker.

## Web accessible resources

A `declarativeNetRequest` rule cannot redirect from a public resource request to a resource that is not web accessible. Doing so triggers an error. This is true even if the specified web accessible resource is owned by the redirecting extension. To declare resources for `declarativeNetRequest`, use the manifest's `"web_accessible_resources"` array.

## Header modification

The `append` operation is only supported for the following headers: `accept`, `accept-encoding`, `accept-language`, `access-control-request-headers`, `cache-control`, `connection`, `content-language`, `cookie`, `forwarded`, `if-match`, `if-none-match`, `keep-alive`, `range`, `te`, `trailer`, `transfer-encoding`, `upgrade`, `user-agent`, `via`, `want-digest`, `x-forwarded-for`.

## Examples

### Code examples

#### Update dynamic rules

The following example shows how to call `updateDynamicRules()`. The procedure for `updateSessionRules()` is the same.

```javascript
// Get arrays containing new and old rules
const newRules = await getNewRules();
const oldRules = await chrome.declarativeNetRequest.getDynamicRules();
const oldRuleIds = oldRules.map(rule => rule.id);

// Use the arrays to update the dynamic rules
await chrome.declarativeNetRequest.updateDynamicRules({
  removeRuleIds: oldRuleIds,
  addRules: newRules
});
```

#### Update static rulesets

The following example shows how to enable and disable rulesets while considering the number of available and the maximum number of enabled static rulesets. You would do this when the number of static rules you need exceeds the number allowed. For this to work, some of your rulesets should be installed with some of your rulesets disabled (setting `"Enabled"` to `false` within the manifest file).

```javascript
async function updateStaticRules(enableRulesetIds, disableCandidateIds) {
  // Create the options structure for the call to updateEnabledRulesets()
  let options = {
    enableRulesetIds: enableRulesetIds
  }

  // Get the number of enabled static rules
  const enabledStaticCount = await chrome.declarativeNetRequest.getEnabledRulesets();

  // Compare rule counts to determine if anything needs to be disabled so that
  // new rules can be enabled
  const proposedCount = enableRulesetIds.length;
  if (enabledStaticCount + proposedCount > chrome.declarativeNetRequest.MAX_NUMBER_OF_ENABLED_STATIC_RULESETS) {
    options.disableRulesetIds = disableCandidateIds
  }

  // Update the enabled static rules
  await chrome.declarativeNetRequest.updateEnabledRulesets(options);
}
```