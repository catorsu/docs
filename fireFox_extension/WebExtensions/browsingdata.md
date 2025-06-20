# BrowsingData

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browsingData
- **Version**: All versions

## Overview
Enables extensions to clear the data that is accumulated while the user is browsing.

In the browsingData API, browsing data is divided into types: browser cache, cookies, downloads, history, local storage, plugin data, saved form data, and saved passwords.

You can use the browsingData.remove() function to remove any combination of these types. There are also dedicated functions to remove each particular type of data, such as removePasswords(), removeHistory() and so on.

## Permissions
- `browsingData` - required

## Types
### DataTypeSet
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| cache | boolean | No | false | The browser's cache |
| cookies | boolean | No | false | Cookies acquired while browsing |
| downloads | boolean | No | false | The browser's download list |
| formData | boolean | No | false | Saved form data |
| history | boolean | No | false | The browser's history |
| indexedDB | boolean | No | false | IndexedDB data |
| localStorage | boolean | No | false | Local storage data |
| passwords | boolean | No | false | Saved passwords |
| pluginData | boolean | No | false | Data associated with plugins |
| serverBoundCertificates | boolean | No | false | Server-bound certificates |
| serviceWorkers | boolean | No | false | Service workers |

### RemovalOptions
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| since | number | No | 0 | Remove data accumulated after this date, represented in milliseconds since the epoch |
| hostnames | Array<string> | No | - | Only remove data associated with these hostnames (applies to cookies, indexedDB, localStorage, and service workers) |
| cookieStoreId | string | No | - | Only remove data associated with a specific cookie store ID (applies to cookies and indexedDB) |
| originTypes | object | No | - | Used to control whether to remove data from normal web pages, hosted apps, and extensions |
| originTypes.unprotectedWeb | boolean | No | true | Normal web pages |
| originTypes.protectedWeb | boolean | No | false | Websites installed as hosted apps |
| originTypes.extension | boolean | No | false | Extensions and packaged apps |

## Methods
### remove()
**Syntax**: `browser.browsingData.remove(removalOptions, dataTypes)`

Removes browsing data for the data types specified.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | Yes | - | Object controlling how far back in time to remove data |
| dataTypes | DataTypeSet | Yes | - | Object describing the types of data to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled with no arguments when the removal has finished

#### Code Examples
```javascript
function onRemoved() {
  console.log("removed");
}

function onError(error) {
  console.error(error);
}

function weekInMilliseconds() {
  return 1000 * 60 * 60 * 24 * 7;
}

var oneWeekAgo = (new Date()).getTime() - weekInMilliseconds();

browser.browsingData.remove(
  {since: oneWeekAgo},
  {downloads: true, history: true}
).then(onRemoved, onError);
```
**Source**: https://frost.cs.uchicago.edu/ref/JavaScript/developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browsingData/remove.html

### removeCache()
**Syntax**: `browser.browsingData.removeCache(removalOptions)`

Clears the browser's cache.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the cache has been cleared

#### Code Examples
No code examples in source documentation

### removeCookies()
**Syntax**: `browser.browsingData.removeCookies(removalOptions)`

Removes cookies.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when cookies have been removed

#### Code Examples
No code examples in source documentation

### removeDownloads()
**Syntax**: `browser.browsingData.removeDownloads(removalOptions)`

Removes the list of downloaded files. Note that this does not delete the downloaded objects themselves, only records of downloads.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when download history has been cleared

#### Code Examples
```javascript
function onRemoved() {
  console.log("removed");
}

function onError(error) {
  console.error(error);
}

function weekInMilliseconds() {
  return 1000 * 60 * 60 * 24 * 7;
}

let oneWeekAgo = new Date().getTime() - weekInMilliseconds();

browser.browsingData.removeDownloads({since: oneWeekAgo})
  .then(onRemoved, onError);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browsingData/removeDownloads

### removeFormData()
**Syntax**: `browser.browsingData.removeFormData(removalOptions)`

Clears saved form data.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when form data has been cleared

#### Code Examples
No code examples in source documentation

### removeHistory()
**Syntax**: `browser.browsingData.removeHistory(removalOptions)`

Clears the browser's history.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when history has been cleared

#### Code Examples
No code examples in source documentation

### removeLocalStorage()
**Syntax**: `browser.browsingData.removeLocalStorage(removalOptions)`

Clears any local storage created by websites.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when local storage has been cleared

#### Code Examples
No code examples in source documentation

### removePasswords()
**Syntax**: `browser.browsingData.removePasswords(removalOptions)`

Clears saved passwords.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when passwords have been cleared

#### Code Examples
No code examples in source documentation

### removePluginData()
**Syntax**: `browser.browsingData.removePluginData(removalOptions)`

Clears data associated with plugins.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| removalOptions | RemovalOptions | No | {} | Object controlling how far back in time to remove data |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when plugin data has been cleared

#### Code Examples
No code examples in source documentation

### settings()
**Syntax**: `browser.browsingData.settings()`

Gets the current value of settings in the browser's "Clear History" feature.

#### Parameters
None

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object containing:
  - `options` - A RemovalOptions object describing the removal options currently selected
  - `dataToRemove` - A DataTypeSet object containing properties for every data type selected for removal
  - `dataRemovalPermitted` - A DataTypeSet object containing properties for every data type permitted for removal

#### Code Examples
```javascript
function onGotSettings(settings) {
  console.log(settings.options);
  console.log(settings.dataToRemove);
  console.log(settings.dataRemovalPermitted);
}

function onError(error) {
  console.error(error);
}

browser.browsingData.settings().then(onGotSettings, onError);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/browsingData/settings

## Events
None

## Related APIs
- `cookies` - For more fine-grained control over cookies
- `history` - For more fine-grained control over history
- `downloads` - For more control over downloads