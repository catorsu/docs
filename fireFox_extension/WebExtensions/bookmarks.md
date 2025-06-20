# Bookmarks

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/bookmarks
- **Version**: All versions

## Overview
The WebExtensions bookmarks API lets an extension interact with and manipulate the browser's bookmarking system. You can use it to bookmark pages, retrieve existing bookmarks, and edit, remove, and organize bookmarks.

Extensions cannot create, modify, or delete bookmarks in the root node of the bookmarks tree. Doing so causes an error with the message: "The bookmark root cannot be modified"

## Permissions
- `bookmarks` - required

## Types
### BookmarkTreeNode
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| id | string | Yes | - | A string which uniquely identifies the node. Each ID is unique within the user's profile |
| parentId | string | No | - | A string which specifies the ID of the parent folder. Not present in the root node |
| index | integer | Yes | - | A zero-based index representing the position of this node within its parent folder |
| url | string | No | - | A string which represents the URL for the bookmark. Omitted for folders |
| title | string | Yes | - | A string which contains the text displayed for the node in menus and lists |
| dateAdded | number | No | - | A number representing the creation date in milliseconds since the epoch |
| dateGroupModified | number | No | - | A number representing when the contents of this folder last changed, in milliseconds |
| unmodifiable | BookmarkTreeNodeUnmodifiable | No | - | Indicates why the node can't be changed. Omitted if the node can be changed |
| type | BookmarkTreeNodeType | No | - | A string indicating whether this is a "bookmark", "folder", or "separator" |
| children | Array<BookmarkTreeNode> | No | - | An ordered array of children. Omitted if the node isn't a folder |

### BookmarkTreeNodeType
| Value | Description |
|-------|-------------|
| "bookmark" | A bookmark |
| "folder" | A folder |
| "separator" | A separator |

### BookmarkTreeNodeUnmodifiable
| Value | Description |
|-------|-------------|
| "managed" | Indicates node was configured by an administrator or supervised user custodian |

### CreateDetails
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| parentId | string | No | Default folder | The ID of the parent folder |
| index | integer | No | - | The position at which to place the new bookmark under its parent |
| title | string | No | - | The title for the bookmark or folder name |
| url | string | No | - | The URL for the bookmark. Omit to create a folder |
| type | BookmarkTreeNodeType | No | "bookmark" | The type of BookmarkTreeNode to create |

## Methods
### create()
**Syntax**: `browser.bookmarks.create(bookmark)`

Creates a bookmark or folder. To create a folder, omit or leave empty the CreateDetails.url parameter.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| bookmark | CreateDetails | Yes | - | An object containing properties for the new bookmark |

#### Returns
- **Type**: `Promise<BookmarkTreeNode>`
- **Description**: Fulfilled with a BookmarkTreeNode describing the newly-created bookmark

#### Code Examples
```javascript
function onBookmarkAdded(bookmarkItem) {
  console.log("Bookmark added with ID: " + bookmarkItem.id);
}

chrome.bookmarks.create({
  title: "bookmarks.create() on MDN",
  url: "https://developer.mozilla.org/Add-ons/WebExtensions/API/bookmarks/create"
}, onBookmarkAdded);
```
**Source**: https://developer.mozilla.org.cach3.com/en-US/docs/Mozilla/Add-ons/WebExtensions/API/bookmarks/create

### get()
**Syntax**: `browser.bookmarks.get(idOrIdList)`

Retrieves one or more BookmarkTreeNodes, given a bookmark's ID or an array of bookmark IDs.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| idOrIdList | string or Array<string> | Yes | - | A string or array of strings specifying the IDs of one or more BookmarkTreeNode objects to retrieve |

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array of BookmarkTreeNode objects, one for each matching node

#### Code Examples
No code examples in source documentation

### getChildren()
**Syntax**: `browser.bookmarks.getChildren(id)`

Retrieves the children of the specified BookmarkTreeNode.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string which specifies the ID of the folder whose children are to be retrieved |

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array of BookmarkTreeNode objects, one for each child node

#### Code Examples
No code examples in source documentation

### getRecent()
**Syntax**: `browser.bookmarks.getRecent(numberOfItems)`

Retrieves a specified number of the most recently added bookmarks.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| numberOfItems | integer | Yes | - | A number representing the maximum number of items to return |

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array of BookmarkTreeNode objects

#### Code Examples
```javascript
function onFulfilled(bookmarks) {
  for (const bookmark of bookmarks) {
    console.log(bookmark.url);
  }
}

function onRejected(error) {
  console.log(`An error: ${error}`);
}

browser.bookmarks.getRecent(1).then(onFulfilled, onRejected);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/bookmarks/getRecent

### getSubTree()
**Syntax**: `browser.bookmarks.getSubTree(id)`

Retrieves part of the bookmarks tree, starting at the specified node. If the item is a folder, you can access all its descendants recursively.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string specifying the ID of the root of the subtree to retrieve |

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array containing one BookmarkTreeNode object representing the item with the given ID

#### Code Examples
No code examples in source documentation

### getTree()
**Syntax**: `browser.bookmarks.getTree()`

Retrieves the entire bookmarks tree into an array of BookmarkTreeNode objects.

#### Parameters
None

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array containing one object, a BookmarkTreeNode representing the root node

#### Code Examples
No code examples in source documentation

### move()
**Syntax**: `browser.bookmarks.move(id, destination)`

Moves the specified BookmarkTreeNode to a new location within the bookmark tree.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string containing the ID of the bookmark or folder to move |
| destination | object | Yes | - | An object specifying the destination for the bookmark |
| destination.parentId | string | No | - | The ID of the destination folder. If omitted, bookmark is moved within current folder |
| destination.index | integer | No | - | A 0-based index specifying the position within the folder |

#### Returns
- **Type**: `Promise<BookmarkTreeNode>`
- **Description**: Fulfilled with a BookmarkTreeNode object describing the moved node

#### Code Examples
No code examples in source documentation

### remove()
**Syntax**: `browser.bookmarks.remove(id)`

Removes a bookmark or an empty bookmark folder, given the node's ID.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string specifying the ID of the bookmark or folder to remove |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled with no arguments when the bookmark has been removed

#### Code Examples
No code examples in source documentation

### removeTree()
**Syntax**: `browser.bookmarks.removeTree(id)`

Recursively removes a bookmark folder and all its contents.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string specifying the ID of the folder node to remove along with its descendants |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled with no arguments when the tree has been removed

#### Code Examples
```javascript
function onRemoved() {
  console.log("bookmark item removed!");
}

function onRejected(error) {
  console.log(`An error: ${error}`);
}

function removeMDN(searchResults) {
  if (searchResults.length) {
    let removing = browser.bookmarks.removeTree(searchResults[0].id);
    removing.then(onRemoved, onRejected);
  }
}

let searchingBookmarks = browser.bookmarks.search({ title: "MDN" });
searchingBookmarks.then(removeMDN, onRejected);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/bookmarks/removeTree

### search()
**Syntax**: `browser.bookmarks.search(query)`

Searches for BookmarkTreeNodes matching a specified set of criteria.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| query | object or string | Yes | - | An object describing the query, or a string to match against URLs and titles |
| query.query | string | No | - | A string matched against bookmark URLs and titles |
| query.url | string | No | - | A string matched against bookmark URLs |
| query.title | string | No | - | A string matched against bookmark titles |

#### Returns
- **Type**: `Promise<Array<BookmarkTreeNode>>`
- **Description**: Fulfilled with an array of BookmarkTreeNode objects, each representing a matching bookmark

#### Code Examples
No code examples in source documentation

### update()
**Syntax**: `browser.bookmarks.update(id, changes)`

Updates the title and/or URL of a bookmark, or the name of a bookmark folder.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| id | string | Yes | - | A string specifying the ID of the bookmark or folder to update |
| changes | object | Yes | - | An object containing the properties to change |
| changes.title | string | No | - | A string containing the new title |
| changes.url | string | No | - | A string containing the new URL |

#### Returns
- **Type**: `Promise<BookmarkTreeNode>`
- **Description**: Fulfilled with a BookmarkTreeNode object representing the updated bookmark

#### Code Examples
No code examples in source documentation

## Events
### onCreated
**Fired when**: A bookmark or folder is created

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| id | string | The ID of the new bookmark |
| bookmark | BookmarkTreeNode | The newly created bookmark |

### onRemoved
**Fired when**: A bookmark or folder is removed. When a folder is removed recursively, a single notification is fired for the folder, and none for its contents

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| id | string | The ID of the removed bookmark |
| removeInfo | object | Object containing additional details |
| removeInfo.parentId | string | The ID of the parent folder |
| removeInfo.index | integer | The zero-based index position in the parent |
| removeInfo.node | BookmarkTreeNode | The removed node |

### onChanged
**Fired when**: A bookmark or folder changes. Currently, only title and url changes trigger this

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| id | string | The ID of the changed bookmark |
| changeInfo | object | Object containing the changed properties |
| changeInfo.title | string | The new title, if changed |
| changeInfo.url | string | The new URL, if changed |

### onMoved
**Fired when**: A bookmark or folder is moved to a different parent folder or to a new offset within its folder

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| id | string | The ID of the moved bookmark |
| moveInfo | object | Object containing move details |
| moveInfo.parentId | string | The ID of the new parent folder |
| moveInfo.index | integer | The new index in the parent folder |
| moveInfo.oldParentId | string | The ID of the old parent folder |
| moveInfo.oldIndex | integer | The old index in the parent folder |

### onChildrenReordered
**Fired when**: The user has sorted the children of a folder in the browser's UI. Not called as a result of move()

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| id | string | The ID of the folder whose children were reordered |
| reorderInfo | object | Currently empty object, reserved for future use |

### onImportBegan
**Fired when**: A bookmark import session is begun. Expensive observers should ignore onCreated updates until onImportEnded is fired

#### Listener Parameters
None

### onImportEnded
**Fired when**: A bookmark import session has finished

#### Listener Parameters
None

## Related APIs
- No directly related APIs listed