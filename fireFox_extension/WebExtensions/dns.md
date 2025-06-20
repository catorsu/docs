# DNS

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/dns
- **Version**: Firefox 60+

## Overview
Enables an extension to resolve domain names.

Note: DNS will fail with NS_ERROR_UNKNOWN_PROXY_HOST if proxying DNS over socks is enabled.

## Permissions
- `dns` - required

## Types
### DNSRecord
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| addresses | Array<string> | Yes | - | Array of IP addresses |
| canonicalName | string | No | - | The canonical hostname for this record |
| isTRR | boolean | Yes | - | True if the resolution was done using DNS-over-HTTPS |

### ResolveFlags
| Value | Description |
|-------|-------------|
| "allow_name_collisions" | Allow name collisions |
| "bypass_cache" | Bypass the DNS cache |
| "canonical_name" | Request the canonical name |
| "disable_ipv4" | Disable IPv4 resolution |
| "disable_ipv6" | Disable IPv6 resolution |
| "disable_trr" | Disable trusted recursive resolver |
| "offline" | Only use cached results |
| "priority_low" | Low priority request |
| "priority_medium" | Medium priority request |
| "speculate" | Speculative resolution |

## Methods
### resolve()
**Syntax**: `browser.dns.resolve(hostname, flags)`

Resolves the given hostname to a DNS record.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| hostname | string | Yes | - | The hostname to resolve |
| flags | Array<ResolveFlags> | No | [] | Resolution flags |

#### Returns
- **Type**: `Promise<DNSRecord>`
- **Description**: Fulfilled with a DNSRecord object

#### Code Examples
```javascript
browser.dns.resolve("example.com").then((record) => {
  console.log(record.addresses);
});

// With flags
browser.dns.resolve("example.com", ["bypass_cache"]).then((record) => {
  console.log("Fresh DNS lookup:", record.addresses);
});
```

## Events
None

## Related APIs
- `proxy` - For configuring proxy settings
- `webRequest` - For intercepting network requests