---
title: chrome.instanceID
url: https://developer.chrome.com/docs/extensions/reference/api/instanceID
---

# chrome.instanceID

## Description

Use `chrome.instanceID` to access the Instance ID service.

## Permissions

`gcm`

## Availability

Chrome 44+

## Methods

### `deleteID()`

Promise

```javascript
chrome.instanceID.deleteID(callback?: function)
```

Resets the app instance identifier and revokes all tokens associated with it.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  () => void
  ```

#### Returns

- `Promise<void>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `deleteToken()`

Promise

```javascript
chrome.instanceID.deleteToken(deleteTokenParams: object, callback?: function)
```

Revokes a granted token.

#### Parameters

- `deleteTokenParams` (object)
  Parameters for `deleteToken`.
  - `authorizedEntity` (string)
    Chrome 46+
    The authorized entity that is used to obtain the token.
  - `scope` (string)
    Chrome 46+
    The scope that is used to obtain the token.
- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  () => void
  ```

#### Returns

- `Promise<void>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getCreationTime()`

Promise

```javascript
chrome.instanceID.getCreationTime(callback?: function)
```

Retrieves the time when the InstanceID has been generated. The creation time will be returned by the callback.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (creationTime: number) => void
  ```
  - `creationTime` (number)
    The time when the Instance ID has been generated, represented in milliseconds since the epoch.

#### Returns

- `Promise<number>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getID()`

Promise

```javascript
chrome.instanceID.getID(callback?: function)
```

Retrieves an identifier for the app instance. The instance ID will be returned by the callback. The same ID will be returned as long as the application identity has not been revoked or expired.

#### Parameters

- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (instanceID: string) => void
  ```
  - `instanceID` (string)
    An Instance ID assigned to the app instance.

#### Returns

- `Promise<string>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getToken()`

Promise

```javascript
chrome.instanceID.getToken(getTokenParams: object, callback?: function)
```

Return a token that allows the authorized entity to access the service defined by scope.

#### Parameters

- `getTokenParams` (object)
  Parameters for `getToken`.
  - `authorizedEntity` (string)
    Chrome 46+
    Identifies the entity that is authorized to access resources associated with this Instance ID. It can be a project ID from Google developer console.
  - `options` (object, optional)
    Chrome 46+ Deprecated since Chrome 89
    `options` are deprecated and will be ignored.
    Allows including a small number of string key/value pairs that will be associated with the token and may be used in processing the request.
  - `scope` (string)
    Chrome 46+
    Identifies authorized actions that the authorized entity can take. E.g. for sending GCM messages, GCM scope should be used.
- `callback` (function, optional)
  The callback parameter looks like:
  ```javascript
  (token: string) => void
  ```
  - `token` (string)
    A token assigned by the requested service.

#### Returns

- `Promise<string>`
  Chrome 96+
  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onTokenRefresh`

```javascript
chrome.instanceID.onTokenRefresh.addListener(callback: function)
```

Fired when all the granted tokens need to be refreshed.

#### Parameters

- `callback` (function)
  The callback parameter looks like:
  ```javascript
  () => void
  ```