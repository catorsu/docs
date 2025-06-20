# storage

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage
- **Version**: Current (as of June 2025)

## Overview

Enables extensions to store and retrieve data, and listen for changes to stored items. The storage system is based on the Web Storage API, with key differences including asynchronous operation, extension-scoped values, support for JSON-ifiable values beyond strings, and multiple key/value pairs per operation.

Although this API is similar to `Window.localStorage`, it is recommended to use the storage API instead. Firefox will clear data stored by extensions using localStorage in various privacy scenarios, while data saved using the storage API will be correctly persisted.

## Permissions

To use this API, include the `"storage"` permission in your manifest.json file:

```json
{
  "permissions": ["storage"]
}
```

## Types

### StorageArea
An object representing a storage area with the following methods:
- `get()` - Retrieves items from storage
- `set()` - Stores items in storage  
- `remove()` - Removes items from storage
- `clear()` - Removes all items from storage
- `getBytesInUse()` - Gets storage space usage

### StorageChange
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| oldValue | any | No | - | The old value of the item, if there was an old value |
| newValue | any | No | - | The new value of the item, if there is a new value |

## Properties

### storage.local
Represents the local storage area. Items in local storage are local to the machine the extension was installed on.

**Usage limits**: Chrome imposes limits on the amount of data that can be stored in local storage.

### storage.managed
Represents the managed storage area. Items in managed storage are set by the domain administrator and are read-only for the extension. Trying to modify this namespace results in an error.

### storage.session
Represents the session storage area. Items in session storage are stored in memory and are not persisted to disk. Data is cleared when the extension is disabled, reloaded, updated, or when the browser restarts.

### storage.sync
Represents the sync storage area. Items in sync storage are synced by the browser and are available across all instances of that browser that the user is logged into, across different devices.

**Usage limits**: 
- Maximum total amount: ~100 KB
- Maximum items: 512
- Maximum item size: 8 KB per item

## Methods

### get()
**Syntax**: `storage.<storageType>.get(keys)`

Retrieves one or more items from the storage area.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| keys | string, array, object, or null | No | null | Key(s) to retrieve. If null/undefined, retrieves all items |

#### Returns
- **Type**: `Promise<object>`
- **Description**: A Promise that resolves to an object containing the retrieved key-value pairs

#### Code Examples
```javascript
// Get all items
browser.storage.local.get().then((result) => {
  console.log(result); // -> Object { kitten: Object, monster: Object }
});

// Get specific item
browser.storage.local.get("kitten").then((result) => {
  console.log(result); // -> Object { kitten: Object }
});

// Get multiple items
browser.storage.local.get(["kitten", "monster"]).then((result) => {
  console.log(result); // -> Object { kitten: Object, monster: Object }
});

// Get with defaults
browser.storage.local.get({
  kitten: "no kitten",
  monster: "no monster"
}).then((result) => {
  console.log(result);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage/StorageArea/get

### set()
**Syntax**: `storage.<storageType>.set(items)`

Stores one or more items in the storage area or updates stored items.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| items | object | Yes | - | Object containing key-value pairs to store |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the operation succeeds

#### Code Examples
```javascript
// Store items
browser.storage.local.set({
  kitten: {name: "Mog", eats: "mice"},
  monster: {name: "Kraken", eats: "people"}
}).then(() => {
  console.log("Items stored successfully");
});

// Update existing item
browser.storage.local.set({
  kitten: {name: "Mog", eats: "fish"}
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage/StorageArea/set

### remove()
**Syntax**: `storage.<storageType>.remove(keys)`

Removes one or more items from the storage area.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| keys | string or array | Yes | - | Key(s) to remove from storage |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the operation succeeds

#### Code Examples
```javascript
// Remove single item
browser.storage.local.remove("kitten");

// Remove multiple items
browser.storage.local.remove(["kitten", "monster"]);
```

### clear()
**Syntax**: `storage.<storageType>.clear()`

Removes all items from the storage area.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when all items are removed

#### Code Examples
```javascript
function onCleared() {
  console.log("Storage cleared");
}

function onError(e) {
  console.log(e);
}

let clearStorage = browser.storage.local.clear();
clearStorage.then(onCleared, onError);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage/StorageArea/clear

### getBytesInUse()
**Syntax**: `storage.<storageType>.getBytesInUse(keys)`

Gets the amount of storage space (in bytes) used for one or more items in the storage area.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| keys | string, array, or null | No | null | Key(s) to check. If null, gets total usage |

#### Returns
- **Type**: `Promise<number>`
- **Description**: A Promise that resolves to the number of bytes used

#### Code Examples
```javascript
// Get total storage usage
browser.storage.local.getBytesInUse().then((bytes) => {
  console.log(`Total storage used: ${bytes} bytes`);
});

// Get usage for specific items
browser.storage.local.getBytesInUse(["kitten", "monster"]).then((bytes) => {
  console.log(`Items use: ${bytes} bytes`);
});
```

## Events

### onChanged
**Fired when**: One or more items change in any of the storage areas

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| changes | object | Object containing changed items with StorageChange values |
| areaName | string | Name of storage area ("local", "sync", "session", or "managed") |

#### Code Examples
```javascript
browser.storage.onChanged.addListener((changes, areaName) => {
  console.log(`Changes in ${areaName}:`);
  for (let key in changes) {
    let change = changes[key];
    console.log(`${key}: old=${change.oldValue}, new=${change.newValue}`);
  }
});
```

## Related APIs
- `sessions` - For persisting data across browser sessions
- `cookies` - For managing browser cookies
- `browserSettings` - For browser-wide settings storage
