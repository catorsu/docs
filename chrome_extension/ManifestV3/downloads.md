---
title: chrome.downloads
url: https://developer.chrome.com/docs/extensions/reference/api/downloads
---

## Description

Use the `chrome.downloads` API to programmatically initiate, monitor, manipulate, and search for downloads.

## Permissions

`downloads`

You must declare the `"downloads"` permission in the extension manifest to use this API.

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "downloads"
  ],
  ...
}
```

## Examples

You can find simple examples of using the `chrome.downloads` API in the `examples/api/downloads` directory. For other examples and for help in viewing the source code, see Samples.

## Types

### `BooleanDelta`

#### Properties

*   `current`

    boolean optional
*   `previous`

    boolean optional

### `DangerType`

*   `file`
    The download's filename is suspicious.
*   `url`
    The download's URL is known to be malicious.
*   `content`
    The downloaded file is known to be malicious.
*   `uncommon`
    The download's URL is not commonly downloaded and could be dangerous.
*   `host`
    The download came from a host known to distribute malicious binaries and is likely dangerous.
*   `unwanted`
    The download is potentially unwanted or unsafe. E.g. it could make changes to browser or computer settings.
*   `safe`
    The download presents no known danger to the user's computer.
*   `accepted`
    The user has accepted the dangerous download.

#### Enum

*   `"file"`
*   `"url"`
*   `"content"`
*   `"uncommon"`
*   `"host"`
*   `"unwanted"`
*   `"safe"`
*   `"accepted"`
*   `"allowlistedByPolicy"`
*   `"asyncScanning"`
*   `"asyncLocalPasswordScanning"`
*   `"passwordProtected"`
*   `"blockedTooLarge"`
*   `"sensitiveContentWarning"`
*   `"sensitiveContentBlock"`
*   `"deepScannedFailed"`
*   `"deepScannedSafe"`
*   `"deepScannedOpenedDangerous"`
*   `"promptForScanning"`
*   `"promptForLocalPasswordScanning"`
*   `"accountCompromise"`
*   `"blockedScanFailed"`

### `DoubleDelta`

#### Properties

*   `current`

    number optional
*   `previous`

    number optional

### `DownloadDelta`

#### Properties

*   `canResume`

    `BooleanDelta` optional

    The change in `canResume`, if any.
*   `danger`

    `StringDelta` optional

    The change in `danger`, if any.
*   `endTime`

    `StringDelta` optional

    The change in `endTime`, if any.
*   `error`

    `StringDelta` optional

    The change in `error`, if any.
*   `exists`

    `BooleanDelta` optional

    The change in `exists`, if any.
*   `fileSize`

    `DoubleDelta` optional

    The change in `fileSize`, if any.
*   `filename`

    `StringDelta` optional

    The change in `filename`, if any.
*   `finalUrl`

    `StringDelta` optional

    Chrome 54+

    The change in `finalUrl`, if any.
*   `id`

    number

    The id of the `DownloadItem` that changed.
*   `mime`

    `StringDelta` optional

    The change in `mime`, if any.
*   `paused`

    `BooleanDelta` optional

    The change in `paused`, if any.
*   `startTime`

    `StringDelta` optional

    The change in `startTime`, if any.
*   `state`

    `StringDelta` optional

    The change in `state`, if any.
*   `totalBytes`

    `DoubleDelta` optional

    The change in `totalBytes`, if any.
*   `url`

    `StringDelta` optional

    The change in `url`, if any.

### `DownloadItem`

#### Properties

*   `byExtensionId`

    string optional

    The identifier for the extension that initiated this download if this download was initiated by an extension. Does not change once it is set.
*   `byExtensionName`

    string optional

    The localized name of the extension that initiated this download if this download was initiated by an extension. May change if the extension changes its name or if the user changes their locale.
*   `bytesReceived`

    number

    Number of bytes received so far from the host, without considering file compression.
*   `canResume`

    boolean

    True if the download is in progress and paused, or else if it is interrupted and can be resumed starting from where it was interrupted.
*   `danger`

    `DangerType`

    Indication of whether this download is thought to be safe or known to be suspicious.
*   `endTime`

    string optional

    The time when the download ended in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){if (item.endTime) console.log(new Date(item.endTime))})})`
*   `error`

    `InterruptReason` optional

    Why the download was interrupted. Several kinds of HTTP errors may be grouped under one of the errors beginning with `SERVER_`. Errors relating to the network begin with `NETWORK_`, errors relating to the process of writing the file to the file system begin with `FILE_`, and interruptions initiated by the user begin with `USER_`.
*   `estimatedEndTime`

    string optional

    Estimated time when the download will complete in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){if (item.estimatedEndTime) console.log(new Date(item.estimatedEndTime))})})`
*   `exists`

    boolean

    Whether the downloaded file still exists. This information may be out of date because Chrome does not automatically watch for file removal. Call `search()` in order to trigger the check for file existence. When the existence check completes, if the file has been deleted, then an `onChanged` event will fire. Note that `search()` does not wait for the existence check to finish before returning, so results from `search()` may not accurately reflect the file system. Also, `search()` may be called as often as necessary, but will not check for file existence any more frequently than once every 10 seconds.
*   `fileSize`

    number

    Number of bytes in the whole file post-decompression, or -1 if unknown.
*   `filename`

    string

    Absolute local path.
*   `finalUrl`

    string

    Chrome 54+

    The absolute URL that this download is being made from, after all redirects.
*   `id`

    number

    An identifier that is persistent across browser sessions.
*   `incognito`

    boolean

    False if this download is recorded in the history, true if it is not recorded.
*   `mime`

    string

    The file's MIME type.
*   `paused`

    boolean

    True if the download has stopped reading data from the host, but kept the connection open.
*   `referrer`

    string

    Absolute URL.
*   `startTime`

    string

    The time when the download began in ISO 8601 format. May be passed directly to the `Date` constructor: `chrome.downloads.search({}, function(items){items.forEach(function(item){console.log(new Date(item.startTime))})})`
*   `state`

    `State`

    Indicates whether the download is progressing, interrupted, or complete.
*   `totalBytes`

    number

    Number of bytes in the whole file, without considering file compression, or -1 if unknown.
*   `url`

    string

    The absolute URL that this download initiated from, before any redirects.

### `DownloadOptions`

#### Properties

*   `body`

    string optional

    Post body.
*   `conflictAction`

    `FilenameConflictAction` optional

    The action to take if `filename` already exists.
*   `filename`

    string optional

    A file path relative to the Downloads directory to contain the downloaded file, possibly containing subdirectories. Absolute paths, empty paths, and paths containing back-references `".."` will cause an error. `onDeterminingFilename` allows suggesting a filename after the file's MIME type and a tentative filename have been determined.
*   `headers`

    `HeaderNameValuePair[]` optional

    Extra HTTP headers to send with the request if the URL uses the HTTP[s] protocol. Each header is represented as a dictionary containing the keys `name` and either `value` or `binaryValue`, restricted to those allowed by `XMLHttpRequest`.
*   `method`

    `HttpMethod` optional

    The HTTP method to use if the URL uses the HTTP[S] protocol.
*   `saveAs`

    boolean optional

    Use a file-chooser to allow the user to select a filename regardless of whether `filename` is set or already exists.
*   `url`

    string

    The URL to download.

### `DownloadQuery`

#### Properties

*   `bytesReceived`

    number optional

    Number of bytes received so far from the host, without considering file compression.
*   `danger`

    `DangerType` optional

    Indication of whether this download is thought to be safe or known to be suspicious.
*   `endTime`

    string optional

    The time when the download ended in ISO 8601 format.
*   `endedAfter`

    string optional

    Limits results to `DownloadItem` that ended after the given ms in ISO 8601 format
*   `endedBefore`

    string optional

    Limits results to `DownloadItem` that ended before the given ms in ISO 8601 format.
*   `error`

    `InterruptReason` optional

    Why a download was interrupted.
*   `exists`

    boolean optional

    Whether the downloaded file exists;
*   `fileSize`

    number optional

    Number of bytes in the whole file post-decompression, or -1 if unknown.
*   `filename`

    string optional

    Absolute local path.
*   `filenameRegex`

    string optional

    Limits results to `DownloadItem` whose `filename` matches the given regular expression.
*   `finalUrl`

    string optional

    Chrome 54+

    The absolute URL that this download is being made from, after all redirects.
*   `finalUrlRegex`

    string optional

    Chrome 54+

    Limits results to `DownloadItem` whose `finalUrl` matches the given regular expression.
*   `id`

    number optional

    The `id` of the `DownloadItem` to query.
*   `limit`

    number optional

    The maximum number of matching `DownloadItem` returned. Defaults to 1000. Set to 0 in order to return all matching `DownloadItem`. See `search` for how to page through results.
*   `mime`

    string optional

    The file's MIME type.
*   `orderBy`

    `string[]` optional

    Set elements of this array to `DownloadItem` properties in order to sort search results. For example, setting `orderBy=['startTime']` sorts the `DownloadItem` by their start time in ascending order. To specify descending order, prefix with a hyphen: `'-startTime'`.
*   `paused`

    boolean optional

    True if the download has stopped reading data from the host, but kept the connection open.
*   `query`

    `string[]` optional

    This array of search terms limits results to `DownloadItem` whose `filename` or `url` or `finalUrl` contain all of the search terms that do not begin with a dash `'-'` and none of the search terms that do begin with a dash.
*   `startTime`

    string optional

    The time when the download began in ISO 8601 format.
*   `startedAfter`

    string optional

    Limits results to `DownloadItem` that started after the given ms in ISO 8601 format.
*   `startedBefore`

    string optional

    Limits results to `DownloadItem` that started before the given ms in ISO 8601 format.
*   `state`

    `State` optional

    Indicates whether the download is progressing, interrupted, or complete.
*   `totalBytes`

    number optional

    Number of bytes in the whole file, without considering file compression, or -1 if unknown.
*   `totalBytesGreater`

    number optional

    Limits results to `DownloadItem` whose `totalBytes` is greater than the given integer.
*   `totalBytesLess`

    number optional

    Limits results to `DownloadItem` whose `totalBytes` is less than the given integer.
*   `url`

    string optional

    The absolute URL that this download initiated from, before any redirects.
*   `urlRegex`

    string optional

    Limits results to `DownloadItem` whose `url` matches the given regular expression.

### `FilenameConflictAction`

*   `uniquify`
    To avoid duplication, the filename is changed to include a counter before the filename extension.
*   `overwrite`
    The existing file will be overwritten with the new file.
*   `prompt`
    The user will be prompted with a file chooser dialog.

#### Enum

*   `"uniquify"`
*   `"overwrite"`
*   `"prompt"`

### `FilenameSuggestion`

#### Properties

*   `conflictAction`

    `FilenameConflictAction` optional

    The action to take if `filename` already exists.
*   `filename`

    string

    The `DownloadItem`'s new target `DownloadItem.filename`, as a path relative to the user's default Downloads directory, possibly containing subdirectories. Absolute paths, empty paths, and paths containing back-references `".."` will be ignored. `filename` is ignored if there are any `onDeterminingFilename` listeners registered by any extensions.

### `GetFileIconOptions`

#### Properties

*   `size`

    number optional

    The size of the returned icon. The icon will be square with dimensions `size` \* `size` pixels. The default and largest size for the icon is 32x32 pixels. The only supported sizes are 16 and 32. It is an error to specify any other size.

### `HeaderNameValuePair`

#### Properties

*   `name`

    string

    Name of the HTTP header.
*   `value`

    string

    Value of the HTTP header.

### `HttpMethod`

#### Enum

*   `"GET"`
*   `"POST"`

### `InterruptReason`

#### Enum

*   `"FILE_FAILED"`
*   `"FILE_ACCESS_DENIED"`
*   `"FILE_NO_SPACE"`
*   `"FILE_NAME_TOO_LONG"`
*   `"FILE_TOO_LARGE"`
*   `"FILE_VIRUS_INFECTED"`
*   `"FILE_TRANSIENT_ERROR"`
*   `"FILE_BLOCKED"`
*   `"FILE_SECURITY_CHECK_FAILED"`
*   `"FILE_TOO_SHORT"`
*   `"FILE_HASH_MISMATCH"`
*   `"FILE_SAME_AS_SOURCE"`
*   `"NETWORK_FAILED"`
*   `"NETWORK_TIMEOUT"`
*   `"NETWORK_DISCONNECTED"`
*   `"NETWORK_SERVER_DOWN"`
*   `"NETWORK_INVALID_REQUEST"`
*   `"SERVER_FAILED"`
*   `"SERVER_NO_RANGE"`
*   `"SERVER_BAD_CONTENT"`
*   `"SERVER_UNAUTHORIZED"`
*   `"SERVER_CERT_PROBLEM"`
*   `"SERVER_FORBIDDEN"`
*   `"SERVER_UNREACHABLE"`
*   `"SERVER_CONTENT_LENGTH_MISMATCH"`
*   `"SERVER_CROSS_ORIGIN_REDIRECT"`
*   `"USER_CANCELED"`
*   `"USER_SHUTDOWN"`
*   `"CRASH"`

### `State`

*   `in_progress`
    The download is currently receiving data from the server.
*   `interrupted`
    An error broke the connection with the file host.
*   `complete`
    The download completed successfully.

#### Enum

*   `"in_progress"`
*   `"interrupted"`
*   `"complete"`

### `StringDelta`

#### Properties

*   `current`

    string optional
*   `previous`

    string optional

### `UiOptions`

Chrome 105+

#### Properties

*   `enabled`

    boolean

    Enable or disable the download UI.

## Methods

### `acceptDanger()`

Promise

```
chrome.downloads.acceptDanger( downloadId: number, callback?: function, )
```

Prompt the user to accept a dangerous download. Can only be called from a visible context (tab, window, or page/browser action popup). Does not automatically accept dangerous downloads. If the download is accepted, then an `onChanged` event will fire, otherwise nothing will happen. When all the data is fetched into a temporary file and either the download is not dangerous or the danger has been accepted, then the temporary file is renamed to the target filename, the state changes to `'complete'`, and `onChanged` fires.

#### Parameters

*   `downloadId`

    number

    The identifier for the `DownloadItem`.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `cancel()`

Promise

```
chrome.downloads.cancel( downloadId: number, callback?: function, )
```

Cancel a download. When `callback` is run, the download is cancelled, completed, interrupted or doesn't exist anymore.

#### Parameters

*   `downloadId`

    number

    The `id` of the download to cancel.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    () => void
    ```

#### Returns

*   `Promise<void>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `download()`

Promise

```
chrome.downloads.download( options: DownloadOptions, callback?: function, )
```

Download a URL. If the URL uses the HTTP[S] protocol, then the request will include all cookies currently set for its hostname. If both `filename` and `saveAs` are specified, then the Save As dialog will be displayed, pre-populated with the specified `filename`. If the download started successfully, `callback` will be called with the new `DownloadItem`'s `downloadId`. If there was an error starting the download, then `callback` will be called with `downloadId=undefined` and `runtime.lastError` will contain a descriptive string. The error strings are not guaranteed to remain backwards compatible between releases. Extensions must not parse it.

#### Parameters

*   `options`

    `DownloadOptions`

    What to download and how.
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (downloadId: number) => void
    ```

    *   `downloadId`

        number

#### Returns

*   `Promise<number>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `erase()`

Promise

```
chrome.downloads.erase( query: DownloadQuery, callback?: function, )
```

Erase matching `DownloadItem` from history without deleting the downloaded file. An `onErased` event will fire for each `DownloadItem` that matches `query`, then `callback` will be called.

#### Parameters

*   `query`

    `DownloadQuery`
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (erasedIds: number[]) => void
    ```

    *   `erasedIds`

        `number[]`

#### Returns

*   `Promise<number[]>`

    Chrome 96+

    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getFileIcon()`

Promise

```
chrome.downloads.getFileIcon( downloadId: number, options?: GetFileIconOptions, callback?: function, )
```

Retrieve an icon for the specified download. For new downloads, file icons are available after the `onCreated` event has been received. The image returned by this function while a download is in progress may be different from the image returned after the download is complete. Icon retrieval is done by querying the underlying operating system or toolkit depending on the platform. The icon that is returned will therefore depend on a number of factors including state of the download, platform, registered file types and visual theme. If a file icon cannot be determined, `runtime.lastError` will contain an error message.

#### Parameters

*   `downloadId`

    number

    The identifier for the download.
*   `options`

    `GetFileIconOptions` optional
*   `callback`

    function optional

    The callback parameter looks like:

    ```
    (iconURL?: string) => void
    ```

    *   `iconURL`

        string optional

#### Returns

*   `Promise<string | undefined>`

    Chrome 96+