# ContextualIdentities

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/contextualIdentities
- **Version**: Firefox 53+

## Overview
Work with contextual identities: list, create, remove, and update contextual identities.

"Contextual identities", also known as "containers", are a browser feature that lets users assume multiple identities when browsing the web, and maintain some separation between these identities. Each contextual identity has a name, a color, and an icon. New tabs can be assigned to an identity, and internally, each identity gets a cookie store that is not shared with other tabs.

Contextual identities are an experimental feature in Firefox and are only enabled by default in Firefox Nightly. To enable them in other versions of Firefox, set the privacy.userContext.enabled preference to true.

## Permissions
- `contextualIdentities` - required
- `cookies` - required

## Types
### ContextualIdentity
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| cookieStoreId | string | Yes | - | The cookie store ID for the identity |
| color | string | Yes | - | The color for the identity ("blue", "turquoise", "green", "yellow", "orange", "red", "pink", "purple", "toolbar") |
| colorCode | string | Yes | - | A hex color code for the identity |
| icon | string | Yes | - | The icon for the identity ("fingerprint", "briefcase", "dollar", "cart", "circle", "gift", "vacation", "food", "fruit", "pet", "tree", "chill", "fence") |
| iconUrl | string | Yes | - | A full resource URL for the identity's icon |
| name | string | Yes | - | The name of the identity |

## Methods
### create()
**Syntax**: `browser.contextualIdentities.create(details)`

Creates a new contextual identity.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | Properties for the new identity |
| details.name | string | Yes | - | The name for the identity |
| details.color | string | Yes | - | The color for the identity |
| details.icon | string | Yes | - | The icon for the identity |

#### Returns
- **Type**: `Promise<ContextualIdentity>`
- **Description**: Fulfilled with a ContextualIdentity describing the new identity

#### Code Examples
No code examples in source documentation

### get()
**Syntax**: `browser.contextualIdentities.get(cookieStoreId)`

Retrieves a contextual identity, given its cookie store ID.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| cookieStoreId | string | Yes | - | The ID of the contextual identity's cookie store |

#### Returns
- **Type**: `Promise<ContextualIdentity>`
- **Description**: Fulfilled with a ContextualIdentity describing the identity

#### Code Examples
No code examples in source documentation

### move()
**Syntax**: `browser.contextualIdentities.move(cookieStoreIds, position)`

Moves one or more contextual identities within the list of contextual identities.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| cookieStoreIds | string or Array<string> | Yes | - | The ID or IDs of the contextual identities to move |
| position | integer | Yes | - | The position to move the identities to |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the identities have been moved

#### Code Examples
No code examples in source documentation

### query()
**Syntax**: `browser.contextualIdentities.query(details)`

Retrieves all contextual identities, or all contextual identities with a particular name.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| details | object | Yes | - | An object to filter identities |
| details.name | string | No | - | Return only identities with this name |

#### Returns
- **Type**: `Promise<Array<ContextualIdentity>>`
- **Description**: Fulfilled with an array of ContextualIdentity objects

#### Code Examples
No code examples in source documentation

### update()
**Syntax**: `browser.contextualIdentities.update(cookieStoreId, details)`

Updates properties of an existing contextual identity.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| cookieStoreId | string | Yes | - | The ID of the contextual identity's cookie store |
| details | object | Yes | - | Properties to change |
| details.name | string | No | - | A new name for the identity |
| details.color | string | No | - | A new color for the identity |
| details.icon | string | No | - | A new icon for the identity |

#### Returns
- **Type**: `Promise<ContextualIdentity>`
- **Description**: Fulfilled with a ContextualIdentity describing the updated identity

#### Code Examples
No code examples in source documentation

### remove()
**Syntax**: `browser.contextualIdentities.remove(cookieStoreId)`

Deletes a contextual identity.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| cookieStoreId | string | Yes | - | The ID of the contextual identity's cookie store |

#### Returns
- **Type**: `Promise<ContextualIdentity>`
- **Description**: Fulfilled with a ContextualIdentity describing the removed identity

#### Code Examples
No code examples in source documentation

## Events
### onCreated
**Fired when**: A contextual identity is created

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| changeInfo | object | Information about the created identity |
| changeInfo.contextualIdentity | ContextualIdentity | The created identity |

### onRemoved
**Fired when**: A contextual identity is removed

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| changeInfo | object | Information about the removed identity |
| changeInfo.contextualIdentity | ContextualIdentity | The removed identity |

### onUpdated
**Fired when**: One or more properties of a contextual identity is updated

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| changeInfo | object | Information about the updated identity |
| changeInfo.contextualIdentity | ContextualIdentity | The updated identity |

## Related APIs
- `cookies` - For working with cookie stores
- `tabs` - For opening tabs in specific containers