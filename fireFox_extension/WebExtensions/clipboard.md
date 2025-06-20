# Clipboard

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/clipboard
- **Version**: Firefox 57+

## Overview
The WebExtension clipboard API (which is different from the standard Clipboard API) enables an extension to copy items to the system clipboard. Currently the WebExtension clipboard API only supports copying images, but it's intended to support copying text and HTML in the future.

The WebExtension clipboard API exists primarily because the standard Clipboard API doesn't support writing images to the clipboard. The WebExtension clipboard API may be deprecated once the standard Clipboard API's support for non-text clipboard contents has entered general use.

Reading from the clipboard is not supported by this API, because the clipboard can already be read using the standard web platform APIs.

## Permissions
- `clipboardWrite` - required

## Types
None

## Methods
### setImageData()
**Syntax**: `browser.clipboard.setImageData(imageData, imageType)`

Copy an image to the clipboard.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| imageData | ArrayBuffer | Yes | - | The image data to be copied to the clipboard |
| imageType | string | Yes | - | The type of the image contained in imageData. Supported types: "png" or "jpeg" |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the image has been copied to the clipboard

#### Code Examples
No code examples in source documentation

## Events
None

## Related APIs
- Standard Clipboard API - For reading from clipboard and text operations
- `contextMenus` - Often used with clipboard operations