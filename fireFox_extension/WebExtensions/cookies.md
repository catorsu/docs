# Cookies

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/cookies
- **Version**: All versions

## Overview
Enables extensions to get, set, and remove cookies, and be notified when they change.

The cookies API provides access to browser cookies with support for tracking protection features including dynamic partitioning (default from Firefox 103) and first-party isolation. Extensions must handle partitioned storage appropriately when working with cookies.

## Permissions
- `cookies` - required API permission
- Host permissions - required for any sites whose cookies you want to access

### Permission Examples
- `http://*.example.com/` - Can read non-secure cookies, write secure/non-secure cookies for www.example.com
- `*://*.example.com/` - Can read/write secure and non-secure cookies for www.example.com

## Types
### Cookie
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| name | string | Yes | - | The name of the cookie |
| value | string | Yes | - | The value of the cookie |
| domain | string | Yes | - | The domain of the cookie |
| hostOnly | boolean | Yes | - | True if the cookie is a host-only cookie |
| path | string | Yes | - | The path of the cookie |
| secure | boolean | Yes | - | True if the cookie is marked as secure |
| httpOnly | boolean | Yes | - | True if the cookie is marked as HttpOnly |
| sameSite | SameSiteStatus | Yes | - | The cookie's same-site status |
| session | boolean | Yes | - | True if the cookie is a session cookie |
| expirationDate | number | No | - | The expiration date of the cookie (seconds since UNIX epoch) |
| storeId | string | Yes | - | The ID of the cookie store containing this cookie |
| firstPartyDomain | string | No | - | The first-party domain of the cookie (when first-party isolation is enabled) |
| partitionKey | object | No | - | The partition key for the cookie (when using dynamic partitioning) |
| partitionKey.topLevelSite | string | No | - | The top-level site for partitioned storage |

### CookieStore
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | string | Yes | - | The unique identifier for the cookie store |
| tabIds | Array<integer> | Yes | - | Array of tab IDs that share this cookie store |
| incognito | boolean | Yes | - | True if this is an incognito cookie store |

### OnChangedCause
| Value | Description |
|-------|-------------|
| "evicted" | Cookie was automatically removed due to garbage collection |
| "expired" | Cookie was automatically removed due to expiry |
| "explicit" | Cookie was inserted or removed via an explicit call |
| "expired_overwrite" | Cookie was overwritten with an already-expired expiration date |
| "overwrite" | Cookie was overwritten by a cookie with the same name |

### SameSiteStatus
| Value | Description |
|-------|-------------|
| "no_restriction" | No SameSite restrictions |
| "lax" | Lax SameSite restrictions |
| "strict" | Strict SameSite restrictions |
| "none" | Explicit SameSite=None |

## Methods
### get()
**Syntax**: `browser.cookies.get(details)`

Retrieves information about a single cookie.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Details to identify the cookie |
| details.url | string | Yes | - | The URL with which the cookie is associated |
| details.name | string | Yes | - | The name of the cookie |
| details.storeId | string | No | Current store | The cookie store to look in |
| details.firstPartyDomain | string | No/Yes* | "" | The first-party domain (*required when first-party isolation is on) |
| details.partitionKey | object | No | - | The partition key for the cookie |

#### Returns
- **Type**: `Promise<Cookie>`
- **Description**: Fulfilled with a Cookie object or null if not found

#### Code Examples
No code examples in source documentation

### getAll()
**Syntax**: `browser.cookies.getAll(details)`

Retrieves all cookies that match a given set of filters.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Object to filter cookies |
| details.url | string | No | - | Restricts cookies to those associated with this URL |
| details.name | string | No | - | Filters cookies by name |
| details.domain | string | No | - | Restricts cookies to a specific domain |
| details.path | string | No | - | Restricts cookies to a specific path |
| details.secure | boolean | No | - | Filters by secure flag |
| details.session | boolean | No | - | Filters session vs persistent cookies |
| details.storeId | string | No | - | Only return cookies from this store |
| details.firstPartyDomain | string | No/Yes* | "" | The first-party domain |
| details.partitionKey | object | No | - | The partition key |

#### Returns
- **Type**: `Promise<Array<Cookie>>`
- **Description**: Fulfilled with an array of Cookie objects

#### Code Examples
No code examples in source documentation

### set()
**Syntax**: `browser.cookies.set(details)`

Sets a cookie with the given cookie data; may overwrite equivalent cookies if they exist.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | The cookie data |
| details.url | string | Yes | - | The request-URI to associate with the cookie |
| details.name | string | No | "" | The name of the cookie |
| details.value | string | No | "" | The value of the cookie |
| details.domain | string | No | Host from URL | The domain of the cookie |
| details.path | string | No | "/" | The path of the cookie |
| details.secure | boolean | No | false | Whether the cookie should be marked as secure |
| details.httpOnly | boolean | No | false | Whether the cookie should be marked as HttpOnly |
| details.sameSite | SameSiteStatus | No | "no_restriction" | The cookie's SameSite status |
| details.expirationDate | number | No | Session | When the cookie should expire (seconds since epoch) |
| details.storeId | string | No | Current store | The cookie store to set the cookie in |
| details.firstPartyDomain | string | No/Yes* | "" | The first-party domain |
| details.partitionKey | object | No | - | The partition key |

#### Returns
- **Type**: `Promise<Cookie>`
- **Description**: Fulfilled with a Cookie object containing details about the cookie that was set

#### Code Examples
No code examples in source documentation

### remove()
**Syntax**: `browser.cookies.remove(details)`

Deletes a cookie by name.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Information to identify the cookie |
| details.url | string | Yes | - | The URL associated with the cookie |
| details.name | string | Yes | - | The name of the cookie to remove |
| details.storeId | string | No | Current store | The cookie store to look in |
| details.firstPartyDomain | string | No/Yes* | "" | The first-party domain |
| details.partitionKey | object | No | - | The partition key |

#### Returns
- **Type**: `Promise<Cookie>`
- **Description**: Fulfilled with a Cookie object containing details about the cookie that was removed, or null if not found

#### Code Examples
No code examples in source documentation

### getAllCookieStores()
**Syntax**: `browser.cookies.getAllCookieStores()`

Lists all existing cookie stores.

#### Parameters
None

#### Returns
- **Type**: `Promise<Array<CookieStore>>`
- **Description**: Fulfilled with an array of CookieStore objects

#### Code Examples
No code examples in source documentation

## Events
### onChanged
**Fired when**: A cookie is set or removed

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| changeInfo | object | Object containing details of the change |
| changeInfo.removed | boolean | True if a cookie was removed, false if added |
| changeInfo.cookie | Cookie | The cookie that was set or removed |
| changeInfo.cause | OnChangedCause | The reason for the change |

## Related APIs
- `privacy` - For controlling first-party isolation
- `browsingData` - For clearing cookies in bulk
- `contextualIdentities` - For working with container tabs and their cookie stores