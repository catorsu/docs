---
title: chrome.webNavigation
url: https://developer.chrome.com/docs/extensions/reference/api/webNavigation
---

# chrome.webNavigation

## Description

Use the `chrome.webNavigation` API to receive notifications about the status of navigation requests in-flight.

## Permissions

`webNavigation`

All `chrome.webNavigation` methods and events require you to declare the "`webNavigation`" permission in the extension manifest. For example:

```json
{ "name": "My extension", ... "permissions": [ "webNavigation" ], ... }
```

## Concepts and usage

### Event order

For a navigation that is successfully completed, events are fired in the following order:

```
onBeforeNavigate -> onCommitted -> [onDOMContentLoaded] -> onCompleted
```

Any error that occurs during the process results in an `onErrorOccurred` event. For a specific navigation, there are no further events fired after `onErrorOccurred`.

If a navigating frame contains subframes, its `onCommitted` is fired before any of its children's `onBeforeNavigate`; while `onCompleted` is fired after all of its children's `onCompleted`.

If the reference fragment of a frame is changed, a `onReferenceFragmentUpdated` event is fired. This event can fire any time after `onDOMContentLoaded`, even after `onCompleted`.

If the history API is used to modify the state of a frame (e.g. using `history.pushState()`, a `onHistoryStateUpdated` event is fired. This event can fire any time after `onDOMContentLoaded`.

If a navigation restored a page from the Back Forward Cache, the `onDOMContentLoaded` event won't fire. The event is not fired because the content has already completed load when the page was first visited.

If a navigation was triggered using Chrome Instant or Instant Pages, a completely loaded page is swapped into the current tab. In that case, an `onTabReplaced` event is fired.

### Relation to webRequest events

There is no defined ordering between events of the `webRequest` API and the events of the `webNavigation` API. It is possible that `webRequest` events are still received for frames that already started a new navigation, or that a navigation only proceeds after the network resources are already fully loaded.

In general, the `webNavigation` events are closely related to the navigation state that is displayed in the UI, while the `webRequest` events correspond to the state of the network stack which is generally opaque to the user.

### Tab IDs

Not all navigating tabs correspond to actual tabs in Chrome's UI, for example, a tab that is being pre-rendered. Such tabs are not accessible using the `tabs` API nor can you request information about them by calling `webNavigation.getFrame()` or `webNavigation.getAllFrames()`. Once such a tab is swapped in, an `onTabReplaced` event is fired and they become accessible through these APIs.

### Timestamps

It's important to note that some technical oddities in the OS's handling of distinct Chrome processes can cause the clock to be skewed between the browser itself and extension processes. That means that the `timeStamp` property of the `WebNavigation` event `timeStamp` property is only guaranteed to be internally consistent. Comparing one event to another event will give you the correct offset between them, but comparing them to the current time inside the extension (using `(new Date()).getTime()`, for instance) might give unexpected results.

### Frame IDs

Frames within a tab can be identified by a frame ID. The frame ID of the main frame is always 0, the ID of child frames is a positive number. Once a document is constructed in a frame, its frame ID remains constant during the lifetime of the document. As of Chrome 49, this ID is also constant for the lifetime of the frame (across multiple navigations).

Due to the multi-process nature of Chrome, a tab might use different processes to render the source and destination of a web page. Therefore, if a navigation takes place in a new process, you might receive events both from the new and the old page until the new navigation is committed (i.e. the `onCommitted` event is sent for the new main frame). In other words, it is possible to have more than one pending sequence of `webNavigation` events with the same `frameId`. The sequences can be distinguished by the `processId` key.

Also note that during a provisional load the process might be switched several times. This happens when the load is redirected to a different site. In this case, you will receive repeated `onBeforeNavigate` and `onErrorOccurred` events, until you receive the final `onCommitted` event.

Another concept that is problematic with extensions is the lifecycle of the frame. A frame hosts a document (which is associated with a committed URL). The document can change (say by navigating) but the `frameId` won't, and so it is difficult to associate that something happened in a specific document with just `frameIds`. We are introducing a concept of a `documentId` which is a unique identifier per document. If a frame is navigated and opens a new document the identifier will change. This field is useful for determining when pages change their lifecycle state (between prerender/active/cached) because it remains the same.

### Transition types and qualifiers

The `webNavigation` `onCommitted` event has a `transitionType` and a `transitionQualifiers` property. The transition type is the same as used in the `history` API describing how the browser navigated to this particular URL. In addition, several transition qualifiers can be returned that further define the navigation.

The following transition qualifiers exist:

| Transition qualifier | Description |
| --- | --- |
| "`client_redirect`" | One or more redirects caused by JavaScript or meta refresh tags on the page happened during the navigation. |
| "`server_redirect`" | One or more redirects caused by HTTP headers sent from the server happened during the navigation. |
| "`forward_back`" | The user used the Forward or Back button to initiate the navigation. |
| "`from_address_bar`" | The user initiated the navigation from the address bar (aka Omnibox). |

## Examples

To try this API, install the `webNavigation` API example from the `chrome-extension-samples` repository.

## Types

### `TransitionQualifier`

Chrome 44+

#### Enum

"`client_redirect`"

"`server_redirect`"

"`forward_back`"

"`from_address_bar`"

### `TransitionType`

Chrome 44+

Cause of the navigation. The same transition types as defined in the `history` API are used. These are the same transition types as defined in the `history` API except with "`start_page`" in place of "`auto_toplevel`" (for backwards compatibility).

#### Enum

"`link`"

"`typed`"

"`auto_bookmark`"

"`auto_subframe`"

"`manual_subframe`"

"`generated`"

"`start_page`"

"`form_submit`"

"`reload`"

"`keyword`"

"`keyword_generated`"

## Methods

### `getAllFrames()`

Promise

```js
chrome.webNavigation.getAllFrames( details: object, callback?: function, )
```

Retrieves information about all frames of a given tab.

#### Parameters

* `details`

  object

  Information about the tab to retrieve all frames from.

  + `tabId`

    number

    The ID of the tab.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (details?: object[]) => void
  ```

  + `details`

    object[] optional

    A list of frames in the given tab, null if the specified tab ID is invalid.

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `errorOccurred`

      boolean

      True if the last navigation in this frame was interrupted by an error, i.e. the `onErrorOccurred` event fired.
    - `frameId`

      number

      The ID of the frame. 0 indicates that this is the main frame; a positive value indicates the ID of a subframe.
    - `frameType`

      `FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `url`

      string

#### Returns

* `Promise<object[] | undefined>`

  Chrome 93+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

### `getFrame()`

Promise

```js
chrome.webNavigation.getFrame( details: object, callback?: function, )
```

Retrieves information about the given frame. A frame refers to an `<iframe>` or a `<frame>` of a web page and is identified by a tab ID and a frame ID.

#### Parameters

* `details`

  object

  Information about the frame to retrieve information about.

  + `documentId`

    string optional

    Chrome 106+

    The UUID of the document. If the `frameId` and/or `tabId` are provided they will be validated to match the document found by provided document ID.
  + `frameId`

    number optional

    The ID of the frame in the given tab.
  + `processId`

    number optional

    Deprecated since Chrome 49

    Frames are now uniquely identified by their tab ID and frame ID; the process ID is no longer needed and therefore ignored.

    The ID of the process that runs the renderer for this tab.
  + `tabId`

    number optional

    The ID of the tab in which the frame is.
* `callback`

  function optional

  The callback parameter looks like:

  ```js
  (details?: object) => void
  ```

  + `details`

    object optional

    Information about the requested frame, null if the specified frame ID and/or tab ID are invalid.

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `errorOccurred`

      boolean

      True if the last navigation in this frame was interrupted by an error, i.e. the `onErrorOccurred` event fired.
    - `frameType`

      `FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `url`

      string

      The URL currently associated with this frame, if the frame identified by the `frameId` existed at one point in the given tab. The fact that an URL is associated with a given `frameId` does not imply that the corresponding frame still exists.

#### Returns

* `Promise<object | undefined>`

  Chrome 93+

  Promises are supported in Manifest V3 and later, but callbacks are provided for backward compatibility. You cannot use both on the same function call. The promise resolves with the same type that is passed to the callback.

## Events

### `onBeforeNavigate`

```js
chrome.webNavigation.onBeforeNavigate.addListener( callback: function, filters?: object, )
```

Fired when a navigation is about to occur.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique for a given tab and process.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      Deprecated since Chrome 50

      The `processId` is no longer set for this event, since the process which will render the resulting document is not known until `onCommit`.

      The value of -1.
    - `tabId`

      number

      The ID of the tab in which the navigation is about to occur.
    - `timeStamp`

      number

      The time when the browser was about to start the navigation, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCommitted`

```js
chrome.webNavigation.onCommitted.addListener( callback: function, filters?: object, )
```

Fired when a navigation is committed. The document (and the resources it refers to, such as images and subframes) might still be downloading, but at least part of the document has been received from the server and the browser has decided to switch to the new document.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCompleted`

```js
chrome.webNavigation.onCompleted.addListener( callback: function, filters?: object, )
```

Fired when a document, including the resources it refers to, is completely loaded and initialized.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the document finished loading, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onCreatedNavigationTarget`

```js
chrome.webNavigation.onCreatedNavigationTarget.addListener( callback: function, filters?: object, )
```

Fired when a new window, or a new tab in an existing window, is created to host a navigation.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `sourceFrameId`

      number

      The ID of the frame with `sourceTabId` in which the navigation is triggered. 0 indicates the main frame.
    - `sourceProcessId`

      number

      The ID of the process that runs the renderer for the source frame.
    - `sourceTabId`

      number

      The ID of the tab in which the navigation is triggered.
    - `tabId`

      number

      The ID of the tab in which the url is opened
    - `timeStamp`

      number

      The time when the browser was about to create a new view, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onDOMContentLoaded`

```js
chrome.webNavigation.onDOMContentLoaded.addListener( callback: function, filters?: object, )
```

Fired when the page's DOM is fully constructed, but the referenced resources may not finish loading.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the page's DOM was fully constructed, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onErrorOccurred`

```js
chrome.webNavigation.onErrorOccurred.addListener( callback: function, filters?: object, )
```

Fired when an error occurs and the navigation is aborted. This can happen if either a network error occurred, or the user aborted the navigation.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `error`

      string

      The error description.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      Deprecated since Chrome 50

      The `processId` is no longer set for this event.

      The value of -1.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the error occurred, in milliseconds since the epoch.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onHistoryStateUpdated`

```js
chrome.webNavigation.onHistoryStateUpdated.addListener( callback: function, filters?: object, )
```

Fired when the frame's history was updated to a new URL. All future events for that frame will use the updated URL.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onReferenceFragmentUpdated`

```js
chrome.webNavigation.onReferenceFragmentUpdated.addListener( callback: function, filters?: object, )
```

Fired when the reference fragment of a frame was updated. All future events for that frame will use the updated URL.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `documentId`

      string

      Chrome 106+

      A UUID of the document loaded.
    - `documentLifecycle`

      `extensionTypes.DocumentLifecycle`

      Chrome 106+

      The lifecycle the document is in.
    - `frameId`

      number

      0 indicates the navigation happens in the tab content window; a positive value indicates navigation in a subframe. Frame IDs are unique within a tab.
    - `frameType`

      `extensionTypes.FrameType`

      Chrome 106+

      The type of frame the navigation occurred in.
    - `parentDocumentId`

      string optional

      Chrome 106+

      A UUID of the parent document owning this frame. This is not set if there is no parent.
    - `parentFrameId`

      number

      Chrome 74+

      The ID of the parent frame, or -1 if this is the main frame.
    - `processId`

      number

      The ID of the process that runs the renderer for this frame.
    - `tabId`

      number

      The ID of the tab in which the navigation occurs.
    - `timeStamp`

      number

      The time when the navigation was committed, in milliseconds since the epoch.
    - `transitionQualifiers`

      `TransitionQualifier[]`

      A list of transition qualifiers.
    - `transitionType`

      `TransitionType`

      Cause of the navigation.
    - `url`

      string
* `filters`

  object optional

  + `url`

    `events.UrlFilter[]`

    Conditions that the URL being navigated to must satisfy. The '`schemes`' and '`ports`' fields of `UrlFilter` are ignored for this event.

### `onTabReplaced`

```js
chrome.webNavigation.onTabReplaced.addListener( callback: function, )
```

Fired when the contents of the tab is replaced by a different (usually previously pre-rendered) tab.

#### Parameters

* `callback`

  function

  The callback parameter looks like:

  ```js
  (details: object) => void
  ```

  + `details`

    object

    - `replacedTabId`

      number

      The ID of the tab that was replaced.
    - `tabId`

      number

      The ID of the tab that replaced the old tab.
    - `timeStamp`

      number

      The time when the replacement happened, in milliseconds since the epoch. 