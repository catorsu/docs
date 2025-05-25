---
title: chrome.fileSystemProvider
url: https://developer.chrome.com/docs/extensions/reference/api/fileSystemProvider
---
**Important: This API works only on ChromeOS.**

## Description

Use the `chrome.fileSystemProvider` API to create file systems, that can be accessible from the file manager on Chrome OS.

## Permissions

`fileSystemProvider`

## Availability

ChromeOS only

You must declare the `"fileSystemProvider"` permission and section in the extension manifest to use the File System Provider API. For example:

```json
{
  "name": "My extension",
  ...
  "permissions": [
    "fileSystemProvider"
  ],
  ...
  "file_system_provider_capabilities": {
    "configurable": true,
    "watchable": false,
    "multiple_mounts": true,
    "source": "network"
  },
  ...
}
```

The `file_system_provider` section must be declared as follows:

*   `configurable` (`boolean`, optional) - Whether configuring via `onConfigureRequested` is supported. By default: `false`.
*   `multiple_mounts` (`boolean`, optional) - Whether multiple (more than one) mounted file systems are supported. By default: `false`.
*   `watchable` (`boolean`, optional) - Whether setting watchers and notifying about changes is supported. By default: `false`.
*   `source` (enum of `"file"`, `"device"`, or `"network"`, required) - Source of data for mounted file systems.

Files app uses above information in order to render related UI elements appropriately. For example, if `configurable` is set to `true`, then a menu item for configuring volumes will be rendered. Similarly, if `multiple_mounts` is set to `true`, then Files app will allow to add more than one mount points from the UI. If `watchable` is `false`, then a refresh button will be rendered. Note, that if possible you should add support for watchers, so changes on the file system can be reflected immediately and automatically.

## Overview

File System Provider API allows extensions to support virtual file systems, which are available in the file manager on ChromeOS. Use cases include decompressing archives and accessing files in a cloud service other than Drive.

## Mounting file systems

Providing extensions can either provide file system contents from an external source (such as a remote server or a USB device), or using a local file (such as an archive) as its input.

In order to write file systems which are file handlers (source is `"file"`) the provider must be a packaged app, as the `onLaunched` event is not available to extensions.

If the source is `network` or a `device`, then the file system should be mounted when `onMountRequested` event is called.

| Source of the file system data | Entry point |
| --- | --- |
| `"file"` | Available to packaged apps only. |
| `"device"` or `"network"` | `onMountRequested` |

## Configuring file systems

Provided file systems once mounted can be configured via the `onConfigureRequested` event. It's especially useful for file systems which provide contents via network in order to set proper credentials. Handling this event is optional.

## Life cycle

Provided file systems once mounted are remembered by Chrome and remounted automatically after reboot or restart. Hence, once a file system is mounted by a providing extension, it will stay until either the extension is unloaded, or the extension calls the `unmount` method.

## Types

### AbortRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `operationRequestId` (`number`)
    An ID of the request to be aborted.
*   `requestId` (`number`)
    The unique identifier of this request.

### Action

Chrome 45+

#### Properties

*   `id` (`string`)
    The identifier of the action. Any string or `CommonActionId` for common actions.
*   `title` (`string`, optional)
    The title of the action. It may be ignored for common actions.

### AddWatcherRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the entry to be observed.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether observing should include all child entries recursively. It can be `true` for directories only.
*   `requestId` (`number`)
    The unique identifier of this request.

### Change

#### Properties

*   `changeType` (`ChangeType`)
    The type of the change which happened to the entry.
*   `cloudFileInfo` (`CloudFileInfo`, optional, Chrome 125+)
    Information relating to the file if backed by a cloud file system.
*   `entryPath` (`string`)
    The path of the changed entry.

### ChangeType

Type of a change detected on the observed directory.

#### Enum

*   `"CHANGED"`
*   `"DELETED"`

### CloseFileRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

### CloudFileInfo

Chrome 125+

#### Properties

*   `versionTag` (`string`, optional)
    A tag that represents the version of the file.

### CloudIdentifier

Chrome 117+

#### Properties

*   `id` (`string`)
    The provider's identifier for the given file/directory.
*   `providerName` (`string`)
    Identifier for the cloud storage provider (e.g. `'drive.google.com'`).

### CommonActionId

Chrome 45+

List of common actions. `"SHARE"` is for sharing files with others. `"SAVE_FOR_OFFLINE"` for pinning (saving for offline access). `"OFFLINE_NOT_NECESSARY"` for notifying that the file doesn't need to be stored for offline access anymore. Used by `onGetActionsRequested` and `onExecuteActionRequested`.

#### Enum

*   `"SAVE_FOR_OFFLINE"`
*   `"OFFLINE_NOT_NECESSARY"`
*   `"SHARE"`

### ConfigureRequestedOptions

Chrome 44+

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be configured.
*   `requestId` (`number`)
    The unique identifier of this request.

### CopyEntryRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `sourcePath` (`string`)
    The source path of the entry to be copied.
*   `targetPath` (`string`)
    The destination path for the copy operation.

### CreateDirectoryRequestedOptions

#### Properties

*   `directoryPath` (`string`)
    The path of the directory to be created.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether the operation is recursive (for directories only).
*   `requestId` (`number`)
    The unique identifier of this request.

### CreateFileRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be created.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### DeleteEntryRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the entry to be deleted.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Whether the operation is recursive (for directories only).
*   `requestId` (`number`)
    The unique identifier of this request.

### EntryMetadata

#### Properties

*   `cloudFileInfo` (`CloudFileInfo`, optional, Chrome 125+)
    Information that identifies a specific file in the underlying cloud file system. Must be provided if requested in options and the file is backed by cloud storage.
*   `cloudIdentifier` (`CloudIdentifier`, optional, Chrome 117+)
    Cloud storage representation of this entry. Must be provided if requested in options and the file is backed by cloud storage. For local files not backed by cloud storage, it should be `undefined` when requested.
*   `isDirectory` (`boolean`, optional)
    `true` if it is a directory. Must be provided if requested in options.
*   `mimeType` (`string`, optional)
    Mime type for the entry. Always optional, but should be provided if requested in options.
*   `modificationTime` (`Date`, optional)
    The last modified time of this entry. Must be provided if requested in options.
*   `name` (`string`, optional)
    Name of this entry (not full path name). Must not contain `'/'`. For root it must be empty. Must be provided if requested in options.
*   `size` (`number`, optional)
    File size in bytes. Must be provided if requested in options.
*   `thumbnail` (`string`, optional)
    Thumbnail image as a data URI in either PNG, JPEG or WEBP format, at most 32 KB in size. Optional, but can be provided only when explicitly requested by the `onGetMetadataRequested` event.

### ExecuteActionRequestedOptions

Chrome 45+

#### Properties

*   `actionId` (`string`)
    The identifier of the action to be executed.
*   `entryPaths` (`string[]`, Chrome 47+)
    The set of paths of the entries to be used for the action.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### FileSystemInfo

#### Properties

*   `displayName` (`string`)
    A human-readable name for the file system.
*   `fileSystemId` (`string`)
    The identifier of the file system.
*   `openedFiles` (`OpenedFile[]`)
    List of currently opened files.
*   `openedFilesLimit` (`number`)
    The maximum number of files that can be opened at once. If `0`, then not limited.
*   `supportsNotifyTag` (`boolean`, optional, Chrome 45+)
    Whether the file system supports the `tag` field for observing directories.
*   `watchers` (`Watcher[]`, Chrome 45+)
    List of watchers.
*   `writable` (`boolean`)
    Whether the file system supports operations which may change contents of the file system (such as creating, deleting or writing to files).

### GetActionsRequestedOptions

Chrome 45+

#### Properties

*   `entryPaths` (`string[]`, Chrome 47+)
    List of paths of entries for the list of actions.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.

### GetMetadataRequestedOptions

#### Properties

*   `cloudFileInfo` (`boolean`, Chrome 125+)
    Set to `true` if `cloudFileInfo` value is requested.
*   `cloudIdentifier` (`boolean`, Chrome 117+)
    Set to `true` if `cloudIdentifier` value is requested.
*   `entryPath` (`string`)
    The path of the entry to fetch metadata about.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `isDirectory` (`boolean`, Chrome 49+)
    Set to `true` if `is_directory` value is requested.
*   `mimeType` (`boolean`, Chrome 49+)
    Set to `true` if `mimeType` value is requested.
*   `modificationTime` (`boolean`, Chrome 49+)
    Set to `true` if `modificationTime` value is requested.
*   `name` (`boolean`, Chrome 49+)
    Set to `true` if `name` value is requested.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `size` (`boolean`, Chrome 49+)
    Set to `true` if `size` value is requested.
*   `thumbnail` (`boolean`)
    Set to `true` if `thumbnail` value is requested.

### MountOptions

#### Properties

*   `displayName` (`string`)
    A human-readable name for the file system.
*   `fileSystemId` (`string`)
    The string indentifier of the file system. Must be unique per each extension.
*   `openedFilesLimit` (`number`, optional)
    The maximum number of files that can be opened at once. If not specified, or `0`, then not limited.
*   `persistent` (`boolean`, optional, Chrome 64+)
    Whether the framework should resume the file system at the next sign-in session. `true` by default.
*   `supportsNotifyTag` (`boolean`, optional, Chrome 45+)
    Whether the file system supports the `tag` field for observed directories.
*   `writable` (`boolean`, optional)
    Whether the file system supports operations which may change contents of the file system (such as creating, deleting or writing to files).

### MoveEntryRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `sourcePath` (`string`)
    The source path of the entry to be moved into a new place.
*   `targetPath` (`string`)
    The destination path for the copy operation.

### NotifyOptions

#### Properties

*   `changeType` (`ChangeType`)
    The type of the change which happened to the observed entry. If it is `DELETED`, then the observed entry will be automatically removed from the list of observed entries.
*   `changes` (`Change[]`, optional)
    List of changes to entries within the observed directory (including the entry itself)
*   `fileSystemId` (`string`)
    The identifier of the file system related to this change.
*   `observedPath` (`string`)
    The path of the observed entry.
*   `recursive` (`boolean`)
    Mode of the observed entry.
*   `tag` (`string`, optional)
    Tag for the notification. Required if the file system was mounted with the `supportsNotifyTag` option. Note, that this flag is necessary to provide notifications about changes which changed even when the system was shutdown.

### OpenedFile

#### Properties

*   `filePath` (`string`)
    The path of the opened file.
*   `mode` (`OpenFileMode`)
    Whether the file was opened for reading or writing.
*   `openRequestId` (`number`)
    A request ID to be be used by consecutive read/write and close requests.

### OpenFileMode

Mode of opening a file. Used by `onOpenFileRequested`.

#### Enum

*   `"READ"`
*   `"WRITE"`

### OpenFileRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be opened.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `mode` (`OpenFileMode`)
    Whether the file will be used for reading or writing.
*   `requestId` (`number`)
    A request ID which will be used by consecutive read/write and close requests.

### ProviderError

Error codes used by providing extensions in response to requests as well as in case of errors when calling methods of the API. For success, `"OK"` must be used.

#### Enum

*   `"OK"`
*   `"FAILED"`
*   `"IN_USE"`
*   `"EXISTS"`
*   `"NOT_FOUND"`
*   `"ACCESS_DENIED"`
*   `"TOO_MANY_OPENED"`
*   `"NO_MEMORY"`
*   `"NO_SPACE"`
*   `"NOT_A_DIRECTORY"`
*   `"INVALID_OPERATION"`
*   `"SECURITY"`
*   `"ABORT"`
*   `"NOT_A_FILE"`
*   `"NOT_EMPTY"`
*   `"INVALID_URL"`
*   `"IO"`

### ReadDirectoryRequestedOptions

#### Properties

*   `directoryPath` (`string`)
    The path of the directory which contents are requested.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `isDirectory` (`boolean`, Chrome 49+)
    Set to `true` if `is_directory` value is requested.
*   `mimeType` (`boolean`, Chrome 49+)
    Set to `true` if `mimeType` value is requested.
*   `modificationTime` (`boolean`, Chrome 49+)
    Set to `true` if `modificationTime` value is requested.
*   `name` (`boolean`, Chrome 49+)
    Set to `true` if `name` value is requested.
*   `requestId` (`number`)
    The unique identifier of this request.
*   `size` (`boolean`, Chrome 49+)
    Set to `true` if `size` value is requested.
*   `thumbnail` (`boolean`, Chrome 49+)
    Set to `true` if `thumbnail` value is requested.

### ReadFileRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `length` (`number`)
    Number of bytes to be returned.
*   `offset` (`number`)
    Position in the file (in bytes) to start reading from.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

### RemoveWatcherRequestedOptions

#### Properties

*   `entryPath` (`string`)
    The path of the watched entry.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `recursive` (`boolean`)
    Mode of the watcher.
*   `requestId` (`number`)
    The unique identifier of this request.

### TruncateRequestedOptions

#### Properties

*   `filePath` (`string`)
    The path of the file to be truncated.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `length` (`number`)
    Number of bytes to be retained after the operation completes.
*   `requestId` (`number`)
    The unique identifier of this request.

### UnmountOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be unmounted.

### UnmountRequestedOptions

#### Properties

*   `fileSystemId` (`string`)
    The identifier of the file system to be unmounted.
*   `requestId` (`number`)
    The unique identifier of this request.

### Watcher

#### Properties

*   `entryPath` (`string`)
    The path of the entry being observed.
*   `lastTag` (`string`, optional)
    Tag used by the last notification for the watcher.
*   `recursive` (`boolean`)
    Whether watching should include all child entries recursively. It can be `true` for directories only.

### WriteFileRequestedOptions

#### Properties

*   `data` (`ArrayBuffer`)
    Buffer of bytes to be written to the file.
*   `fileSystemId` (`string`)
    The identifier of the file system related to this operation.
*   `offset` (`number`)
    Position in the file (in bytes) to start writing the bytes from.
*   `openRequestId` (`number`)
    A request ID used to open the file.
*   `requestId` (`number`)
    The unique identifier of this request.

## Methods

### get()

Promise

```
chrome.fileSystemProvider.get( fileSystemId: string, callback?: function, )
```

Returns information about a file system with the passed `fileSystemId`.

#### Parameters

*   `fileSystemId` (`string`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (fileSystem: FileSystemInfo) => void
    ```
    *   `fileSystem` (`FileSystemInfo`)

#### Returns

*   `Promise<FileSystemInfo>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### getAll()

Promise

```
chrome.fileSystemProvider.getAll( callback?: function, )
```

Returns all file systems mounted by the extension.

#### Parameters

*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    (fileSystems: FileSystemInfo[]) => void
    ```
    *   `fileSystems` (`FileSystemInfo[]`)

#### Returns

*   `Promise<FileSystemInfo[]>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### mount()

Promise

```
chrome.fileSystemProvider.mount( options: MountOptions, callback?: function, )
```

Mounts a file system with the given `options`.

#### Parameters

*   `options` (`MountOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### notify()

Promise

```
chrome.fileSystemProvider.notify( options: NotifyOptions, callback?: function, )
```

Notifies about a change in the watched directory.

#### Parameters

*   `options` (`NotifyOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### unmount()

Promise

```
chrome.fileSystemProvider.unmount( options: UnmountOptions, callback?: function, )
```

Unmounts a file system with the given `fileSystemId`.

#### Parameters

*   `options` (`UnmountOptions`)
*   `callback` (`function`, optional)
    The callback parameter looks like:
    ```
    () => void
    ```

#### Returns

*   `Promise<void>` (Chrome 96+)
    Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### onAbortRequested

```
chrome.fileSystemProvider.onAbortRequested.addListener(
  callback: (options: AbortRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to abort an operation is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: AbortRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`AbortRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onAddWatcherRequested

```
chrome.fileSystemProvider.onAddWatcherRequested.addListener(
  callback: (options: AddWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to add a new watcher is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: AddWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`AddWatcherRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCloseFileRequested

```
chrome.fileSystemProvider.onCloseFileRequested.addListener(
  callback: (options: CloseFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to close a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CloseFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CloseFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onConfigureRequested

Chrome 44+

```
chrome.fileSystemProvider.onConfigureRequested.addListener(
  callback: (options: ConfigureRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to configure a mounted file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ConfigureRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`ConfigureRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCopyEntryRequested

```
chrome.fileSystemProvider.onCopyEntryRequested.addListener(
  callback: (options: CopyEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to copy an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CopyEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CopyEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCreateDirectoryRequested

```
chrome.fileSystemProvider.onCreateDirectoryRequested.addListener(
  callback: (options: CreateDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to create a directory is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CreateDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CreateDirectoryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onCreateFileRequested

```
chrome.fileSystemProvider.onCreateFileRequested.addListener(
  callback: (options: CreateFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to create a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: CreateFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`CreateFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onDeleteEntryRequested

```
chrome.fileSystemProvider.onDeleteEntryRequested.addListener(
  callback: (options: DeleteEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to delete an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: DeleteEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`DeleteEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onExecuteActionRequested

Chrome 45+

```
chrome.fileSystemProvider.onExecuteActionRequested.addListener(
  callback: (options: ExecuteActionRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to execute an action is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ExecuteActionRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`ExecuteActionRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onGetActionsRequested

Chrome 45+

```
chrome.fileSystemProvider.onGetActionsRequested.addListener(
  callback: (options: GetActionsRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to get a list of actions for a set of entries is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: GetActionsRequestedOptions, successCallback: (actions: Action[]) => void, errorCallback: function) => void
    ```
    *   `options` (`GetActionsRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (actions: Action[]) => void
        ```
        *   `actions` (`Action[]`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onGetMetadataRequested

```
chrome.fileSystemProvider.onGetMetadataRequested.addListener(
  callback: (options: GetMetadataRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to get metadata of an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: GetMetadataRequestedOptions, successCallback: (metadata: EntryMetadata) => void, errorCallback: function) => void
    ```
    *   `options` (`GetMetadataRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (metadata: EntryMetadata) => void
        ```
        *   `metadata` (`EntryMetadata`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onMountRequested

Chrome 44+

```
chrome.fileSystemProvider.onMountRequested.addListener(
  callback: (successCallback: function, errorCallback: function) => void
)
```

Raised when a request to mount a new file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (successCallback: function, errorCallback: function) => void
    ```
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onMoveEntryRequested

```
chrome.fileSystemProvider.onMoveEntryRequested.addListener(
  callback: (options: MoveEntryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to move an entry is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: MoveEntryRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`MoveEntryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onOpenFileRequested

```
chrome.fileSystemProvider.onOpenFileRequested.addListener(
  callback: (options: OpenFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to open a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: OpenFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`OpenFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onReadDirectoryRequested

```
chrome.fileSystemProvider.onReadDirectoryRequested.addListener(
  callback: (options: ReadDirectoryRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to read a directory is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ReadDirectoryRequestedOptions, successCallback: (entries: EntryMetadata[], hasMore: boolean) => void, errorCallback: function) => void
    ```
    *   `options` (`ReadDirectoryRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (entries: EntryMetadata[], hasMore: boolean) => void
        ```
        *   `entries` (`EntryMetadata[]`)
        *   `hasMore` (`boolean`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onReadFileRequested

```
chrome.fileSystemProvider.onReadFileRequested.addListener(
  callback: (options: ReadFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to read a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: ReadFileRequestedOptions, successCallback: (data: ArrayBuffer, hasMore: boolean) => void, errorCallback: function) => void
    ```
    *   `options` (`ReadFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully. The callback parameter looks like:
        ```
        (data: ArrayBuffer, hasMore: boolean) => void
        ```
        *   `data` (`ArrayBuffer`)
        *   `hasMore` (`boolean`)
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onRemoveWatcherRequested

```
chrome.fileSystemProvider.onRemoveWatcherRequested.addListener(
  callback: (options: RemoveWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to remove a watcher is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: RemoveWatcherRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`RemoveWatcherRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onTruncateRequested

```
chrome.fileSystemProvider.onTruncateRequested.addListener(
  callback: (options: TruncateRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to truncate a file to a new size is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: TruncateRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`TruncateRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onUnmountRequested

```
chrome.fileSystemProvider.onUnmountRequested.addListener(
  callback: (options: UnmountRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to unmount a file system is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: UnmountRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`UnmountRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)

### onWriteFileRequested

```
chrome.fileSystemProvider.onWriteFileRequested.addListener(
  callback: (options: WriteFileRequestedOptions, successCallback: function, errorCallback: function) => void
)
```

Raised when a request to write to a file is invoked.

#### Parameters

*   `callback` (`function`)
    The callback parameter looks like:
    ```
    (options: WriteFileRequestedOptions, successCallback: function, errorCallback: function) => void
    ```
    *   `options` (`WriteFileRequestedOptions`)
    *   `successCallback` (`function`)
        A callback to be called when the operation is finished successfully.
    *   `errorCallback` (`function`)
        A callback to be called when the operation failed. The callback parameter looks like:
        ```
        (error: ProviderError) => void
        ```
        *   `error` (`ProviderError`)