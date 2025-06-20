# Downloads

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads
- **Version**: All versions

## Overview
Enables extensions to interact with the browser's download manager. You can use this API module to download files, cancel, pause, resume downloads, and show downloaded files in the file manager.

## Permissions
- `downloads` - required

## Types
### DownloadItem
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | integer | Yes | - | An integer representing a unique identifier for the downloaded file |
| url | string | Yes | - | The absolute URL that the download was initiated from |
| referrer | string | No | - | The absolute URL of the referrer |
| filename | string | Yes | - | Absolute local path |
| incognito | boolean | Yes | - | Whether the download is recorded in history |
| cookieStoreId | string | No | - | The cookie store ID of the contextual identity |
| danger | DangerType | Yes | - | Indication of whether the download is thought to be safe or known to be suspicious |
| mime | string | No | - | The file's MIME type |
| startTime | string | Yes | - | When the download began (ISO 8601 format) |
| endTime | string | No | - | When the download ended (ISO 8601 format) |
| estimatedEndTime | string | No | - | Estimated time when download will complete (ISO 8601 format) |
| state | State | Yes | - | The download's current state |
| paused | boolean | Yes | - | True if the download has stopped reading data but kept the connection open |
| canResume | boolean | Yes | - | Whether a paused download can be resumed |
| error | InterruptReason | No | - | Why the download was interrupted |
| bytesReceived | number | Yes | - | Number of bytes received so far |
| totalBytes | number | Yes | - | Total number of bytes in the file (-1 if unknown) |
| fileSize | number | Yes | - | Number of bytes in the file after decompression (-1 if unknown) |
| exists | boolean | Yes | - | Whether the downloaded file still exists |
| byExtensionId | string | No | - | The ID of the extension that triggered the download |
| byExtensionName | string | No | - | The name of the extension that triggered the download |

### FilenameConflictAction
| Value | Description |
|-------|-------------|
| "uniquify" | The browser will modify the filename to make it unique |
| "overwrite" | The browser will overwrite the existing file |
| "prompt" | The browser will prompt the user |

### InterruptReason
| Value | Description |
|-------|-------------|
| "FILE_FAILED" | General file error |
| "FILE_ACCESS_DENIED" | File access denied |
| "FILE_NO_SPACE" | Not enough free disk space |
| "FILE_NAME_TOO_LONG" | File name too long |
| "FILE_TOO_LARGE" | File too large |
| "FILE_VIRUS_INFECTED" | File is virus infected |
| "FILE_TRANSIENT_ERROR" | Temporary problem with file |
| "FILE_BLOCKED" | File blocked by local policy |
| "FILE_SECURITY_CHECK_FAILED" | Security check failed |
| "FILE_TOO_SHORT" | File too short |
| "NETWORK_FAILED" | General network error |
| "NETWORK_TIMEOUT" | Network timeout |
| "NETWORK_DISCONNECTED" | Network disconnected |
| "NETWORK_SERVER_DOWN" | Server down |
| "NETWORK_INVALID_REQUEST" | Invalid network request |
| "SERVER_FAILED" | General server error |
| "SERVER_NO_RANGE" | Server doesn't support range requests |
| "SERVER_BAD_CONTENT" | Server sent bad content |
| "SERVER_UNAUTHORIZED" | Server unauthorized |
| "SERVER_CERT_PROBLEM" | Server certificate problem |
| "SERVER_FORBIDDEN" | Server forbidden |
| "USER_CANCELED" | User canceled |
| "USER_SHUTDOWN" | User shut down browser |
| "CRASH" | Browser crashed |

### DangerType
| Value | Description |
|-------|-------------|
| "file" | The download's filename is suspicious |
| "url" | The download's URL is known to be malicious |
| "content" | The downloaded file is known to be malicious |
| "uncommon" | The download's URL is not commonly downloaded |
| "host" | The download came from a host known to distribute malicious binaries |
| "unwanted" | The download is potentially unwanted or unsafe |
| "safe" | The download presents no known danger |
| "accepted" | The user has accepted the dangerous download |

### State
| Value | Description |
|-------|-------------|
| "in_progress" | The download is currently receiving data |
| "interrupted" | An error interrupted the download |
| "complete" | The download completed successfully |

### DownloadQuery
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| query | Array<string> | No | - | Array of terms to match against filename and URL |
| startedBefore | DownloadTime | No | - | Include only downloads started before this time |
| startedAfter | DownloadTime | No | - | Include only downloads started after this time |
| endedBefore | DownloadTime | No | - | Include only downloads ended before this time |
| endedAfter | DownloadTime | No | - | Include only downloads ended after this time |
| totalBytesGreater | number | No | - | Include only downloads with totalBytes greater than this |
| totalBytesLess | number | No | - | Include only downloads with totalBytes less than this |
| filenameRegex | string | No | - | Regular expression to match against filename |
| urlRegex | string | No | - | Regular expression to match against URL |
| limit | integer | No | - | Maximum number of results |
| orderBy | Array<string> | No | - | Sort order (e.g., ["-startTime"]) |
| id | integer | No | - | The ID of a specific download |
| url | string | No | - | Absolute URL to match |
| filename | string | No | - | Absolute local path to match |
| danger | DangerType | No | - | DangerType to match |
| mime | string | No | - | MIME type to match |
| startTime | string | No | - | Start time to match |
| endTime | string | No | - | End time to match |
| state | State | No | - | State to match |
| paused | boolean | No | - | Paused state to match |
| error | InterruptReason | No | - | InterruptReason to match |
| bytesReceived | number | No | - | Number of bytes received to match |
| totalBytes | number | No | - | Total bytes to match |
| fileSize | number | No | - | File size to match |
| exists | boolean | No | - | Existence state to match |
| cookieStoreId | string | No | - | Cookie store ID to match |

### StringDelta
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| previous | string | No | - | The previous value |
| current | string | No | - | The current value |

### DoubleDelta
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| previous | number | No | - | The previous value |
| current | number | No | - | The current value |

### BooleanDelta
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| previous | boolean | No | - | The previous value |
| current | boolean | No | - | The current value |

## Methods
### download()
**Syntax**: `browser.downloads.download(options)`

Downloads a file, given its URL and other optional preferences.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| options | object | Yes | - | Download options |
| options.url | string | Yes | - | The URL to download |
| options.filename | string | No | - | Path relative to the default Downloads directory |
| options.conflictAction | FilenameConflictAction | No | "uniquify" | Action to take if filename already exists |
| options.saveAs | boolean | No | false | Whether to prompt the user with a Save As dialog |
| options.method | string | No | "GET" | The HTTP method to use |
| options.headers | Array<object> | No | - | Extra HTTP headers to send |
| options.body | string | No | - | Post body |
| options.allowHttpErrors | boolean | No | false | Whether to proceed with download on HTTP errors |
| options.incognito | boolean | No | - | Whether to associate with private browsing |
| options.cookieStoreId | string | No | - | The cookie store ID to associate with |

#### Returns
- **Type**: `Promise<integer>`
- **Description**: Fulfilled with the ID of the new download

#### Code Examples
```javascript
function onStartedDownload(id) {
  console.log(`Started downloading: ${id}`);
}

function onFailed(error) {
  console.log(`Download failed: ${error}`);
}

const downloadUrl = "https://example.org/image.png";

const downloading = browser.downloads.download({
  url : downloadUrl,
  filename : 'my-image.png',
  conflictAction : 'uniquify'
});

downloading.then(onStartedDownload, onFailed);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/download

### search()
**Syntax**: `browser.downloads.search(query)`

Queries the DownloadItems available in the browser's downloads manager.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| query | DownloadQuery | Yes | - | A query to filter results |

#### Returns
- **Type**: `Promise<Array<DownloadItem>>`
- **Description**: Array of DownloadItem objects matching the query

#### Code Examples
```javascript
function logDownloads(downloads) {
  for (const download of downloads) {
    console.log(download.url);
  }
}

function onError(error) {
  console.log(`Error: ${error}`);
}

const searching = browser.downloads.search({
  limit: 10,
  orderBy: ["-startTime"]
});

searching.then(logDownloads, onError);
```
**Source**: https://developer.mozilla.org.cach3.com/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/search

### pause()
**Syntax**: `browser.downloads.pause(downloadId)`

Pauses a download.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to pause |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the download has been paused

#### Code Examples
No code examples in source documentation

### resume()
**Syntax**: `browser.downloads.resume(downloadId)`

Resumes a paused download.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to resume |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the download has been resumed

#### Code Examples
No code examples in source documentation

### cancel()
**Syntax**: `browser.downloads.cancel(downloadId)`

Cancels a download.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to cancel |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the download has been canceled

#### Code Examples
No code examples in source documentation

### getFileIcon()
**Syntax**: `browser.downloads.getFileIcon(downloadId, options)`

Retrieves an icon for the specified download.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download |
| options | object | No | - | Options object |
| options.size | integer | No | 32 | Size of the icon (16 or 32) |

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with the icon URL

#### Code Examples
No code examples in source documentation

### open()
**Syntax**: `browser.downloads.open(downloadId)`

Opens the downloaded file with its associated application.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to open |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the file has been opened

#### Code Examples
No code examples in source documentation

### show()
**Syntax**: `browser.downloads.show(downloadId)`

Opens the platform's file manager to show the downloaded file.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to show |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: Fulfilled with true if successful

#### Code Examples
No code examples in source documentation

### showDefaultFolder()
**Syntax**: `browser.downloads.showDefaultFolder()`

Opens the platform's file manager to show the default downloads folder.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the folder is shown

#### Code Examples
No code examples in source documentation

### erase()
**Syntax**: `browser.downloads.erase(query)`

Erases matching DownloadItems from the browser's download history.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| query | DownloadQuery | Yes | - | A query to filter items to erase |

#### Returns
- **Type**: `Promise<Array<integer>>`
- **Description**: Array of erased download IDs

#### Code Examples
```javascript
function handleErased(erasedIds) {
  console.log(`Erased: ${erasedIds}`);
}

const erasing = browser.downloads.erase({
  limit: 1,
  orderBy: ["-startTime"]
});

erasing.then(handleErased);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/onErased

### removeFile()
**Syntax**: `browser.downloads.removeFile(downloadId)`

Removes a downloaded file from disk, but not from the browser's download history.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the download to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the file has been removed

#### Code Examples
No code examples in source documentation

### acceptDanger()
**Syntax**: `browser.downloads.acceptDanger(downloadId)`

Prompts the user to accept or cancel a dangerous download.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| downloadId | integer | Yes | - | The ID of the dangerous download |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the danger prompt has been shown

#### Code Examples
No code examples in source documentation

### setShelfEnabled()
**Syntax**: `browser.downloads.setShelfEnabled(enabled)`

Enables or disables the gray shelf at the bottom of every window.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| enabled | boolean | Yes | - | Whether to enable the shelf |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the setting has been changed

#### Code Examples
No code examples in source documentation

## Events
### onCreated
**Fired when**: A download begins

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| downloadItem | DownloadItem | The DownloadItem object in question |

#### Code Examples
```javascript
function handleCreated(item) {
  console.log(item.url);
}

browser.downloads.onCreated.addListener(handleCreated);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/onCreated

### onErased
**Fired when**: A download is erased from history

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| downloadId | integer | The ID of the erased download |

#### Code Examples
```javascript
function handleErased(item) {
  console.log(`Erased: ${item}`);
}

browser.downloads.onErased.addListener(handleErased);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/onErased

### onChanged
**Fired when**: Any of a DownloadItem's properties changes (except bytesReceived)

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| downloadDelta | object | Object describing what changed |
| downloadDelta.id | integer | The ID of the DownloadItem that changed |
| downloadDelta.url | StringDelta | Change in url |
| downloadDelta.filename | StringDelta | Change in filename |
| downloadDelta.danger | StringDelta | Change in danger |
| downloadDelta.mime | StringDelta | Change in mime |
| downloadDelta.startTime | StringDelta | Change in startTime |
| downloadDelta.endTime | StringDelta | Change in endTime |
| downloadDelta.state | StringDelta | Change in state |
| downloadDelta.canResume | BooleanDelta | Change in canResume |
| downloadDelta.paused | BooleanDelta | Change in paused |
| downloadDelta.error | StringDelta | Change in error |
| downloadDelta.totalBytes | DoubleDelta | Change in totalBytes |
| downloadDelta.fileSize | DoubleDelta | Change in fileSize |
| downloadDelta.exists | BooleanDelta | Change in exists |

#### Code Examples
```javascript
function handleChanged(delta) {
  if (delta.state && delta.state.current === "complete") {
    console.log(`Download ${delta.id} has completed.`);
  }
}

browser.downloads.onChanged.addListener(handleChanged);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/downloads/onChanged

## Related APIs
- `browsingData` - For clearing download history
- `webRequest` - For monitoring network requests
- `tabs` - For associating downloads with tabs