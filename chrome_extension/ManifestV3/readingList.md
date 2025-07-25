---
title: chrome.readingList
url: https://developer.chrome.com/docs/extensions/reference/api/readingList
---

# chrome.readingList

## Description

Use the `chrome.readingList` API to read from and modify the items in the Reading List.

## Permissions

`readingList`

To use the Reading List API, add the "readingList" permission in the extension manifest file:

manifest.json:

```json
{
  "name": "My reading list extension",
  ...
  "permissions": [
    "readingList"
  ]
}
```

## Availability

Chrome 120+ MV3+

Chrome features a reading list located on the side panel. It lets users save web pages to read later or when offline. Use the Reading List API to retrieve existing items and add or remove items from the list.

Reading list showing a number of articles

## Concepts and usage

### Item ordering

Items in the reading list are not in any guaranteed order.

### Item uniqueness

Items are keyed by URL. This includes the hash and query string.

## Use cases

The following sections demonstrate some common use cases for the Reading List API. See Extension samples for complete extension examples.

### Add an item

To add an item to the reading list, use `chrome.readingList.addEntry()`:

```javascript
chrome.readingList.addEntry({
  title: "New to the web platform in September | web.dev",
  url: "https://developer.chrome.com/",
  hasBeenRead: false
});
```

### Display items

To display items from the reading list, use the `chrome.readingList.query()` method to retrieve them. method.

```javascript
const items = await chrome.readingList.query({});
for (const item of items) {
  // Do something do display the item
}
```

### Mark an item as read

You can use `chrome.readingList.updateEntry()` to update the title, URL, and read status. The following code marks an item as read:

```javascript
chrome.readingList.updateEntry({
  url: "https://developer.chrome.com/",
  hasBeenRead: true
});
```

### Remove an item

To remove an item, use `chrome.readingList.removeEntry()`:

```javascript
chrome.readingList.removeEntry({ url: "https://developer.chrome.com/" });
```

## Extension samples

For more Reading List API extensions demos, see the Reading List API sample.

## Types

### AddEntryOptions

#### Properties

*   `hasBeenRead`
    boolean
    Will be `true` if the entry has been read.
*   `title`
    string
    The title of the entry.
*   `url`
    string
    The url of the entry.

### QueryInfo

#### Properties

*   `hasBeenRead`
    boolean optional
    Indicates whether to search for read (`true`) or unread (`false`) items.
*   `title`
    string optional
    A title to search for.
*   `url`
    string optional
    A url to search for.

### ReadingListEntry

#### Properties

*   `creationTime`
    number
    The time the entry was created. Recorded in milliseconds since Jan 1, 1970.
*   `hasBeenRead`
    boolean
    Will be `true` if the entry has been read.
*   `lastUpdateTime`
    number
    The last time the entry was updated. This value is in milliseconds since Jan 1, 1970.
*   `title`
    string
    The title of the entry.
*   `url`
    string
    The url of the entry.

### RemoveOptions

#### Properties

*   `url`
    string
    The url to remove.

### UpdateEntryOptions

#### Properties

*   `hasBeenRead`
    boolean optional
    The updated read status. The existing status remains if a value isn't provided.
*   `title`
    string optional
    The new title. The existing tile remains if a value isn't provided.
*   `url`
    string
    The url that will be updated.

## Methods

### addEntry()

Promise

```
chrome.readingList.addEntry(
  entry: AddEntryOptions,
  callback?: function,
)
```

Adds an entry to the reading list if it does not exist.

#### Parameters

*   `entry`
    `AddEntryOptions`
    The entry to add to the reading list.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### query()

Promise

```
chrome.readingList.query(
  info: QueryInfo,
  callback?: function,
)
```

Retrieves all entries that match the `QueryInfo` properties. Properties that are not provided will not be matched.

#### Parameters

*   `info`
    `QueryInfo`
    The properties to search for.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    (entries: ReadingListEntry[]) => void
    ```
    *   `entries`
        `ReadingListEntry`[]

#### Returns

*   Promise&lt;`ReadingListEntry`[]&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### removeEntry()

Promise

```
chrome.readingList.removeEntry(
  info: RemoveOptions,
  callback?: function,
)
```

Removes an entry from the reading list if it exists.

#### Parameters

*   `info`
    `RemoveOptions`
    The entry to remove from the reading list.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### updateEntry()

Promise

```
chrome.readingList.updateEntry(
  info: UpdateEntryOptions,
  callback?: function,
)
```

Updates a reading list entry if it exists.

#### Parameters

*   `info`
    `UpdateEntryOptions`
    The entry to update.
*   `callback`
    function optional
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   Promise&lt;void&gt;
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onEntryAdded

```
chrome.readingList.onEntryAdded.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is added to the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry`

### onEntryRemoved

```
chrome.readingList.onEntryRemoved.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is removed from the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry`

### onEntryUpdated

```
chrome.readingList.onEntryUpdated.addListener(
  callback: function,
)
```

Triggered when a `ReadingListEntry` is updated in the reading list.

#### Parameters

*   `callback`
    function
    The callback parameter looks like:
    ```
    (entry: ReadingListEntry) => void
    ```
    *   `entry`
        `ReadingListEntry` 