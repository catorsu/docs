# ExtensionTypes

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/extensionTypes
- **Version**: All versions

## Overview
Some common types used in other WebExtension APIs. This API provides shared type definitions that are used across multiple extension APIs, particularly for image handling and script/CSS injection.

## Permissions
- No special permissions required

## Types
### ImageDetails
Details about the format, quality, area and scale of a captured image.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| format | ImageFormat | No | "png" | The format of the resulting image |
| quality | integer | No | 92 | When format is "jpeg", quality level between 0 and 100 |
| rect | object | No | - | Area to capture. If omitted, captures visible viewport |
| rect.x | number | Yes | - | X coordinate |
| rect.y | number | Yes | - | Y coordinate |
| rect.width | number | Yes | - | Width |
| rect.height | number | Yes | - | Height |
| scale | number | No | devicePixelRatio | Scale to apply. Defaults to devicePixelRatio |

### ImageFormat
The format of an image.

| Value | Description |
|-------|-------------|
| "jpeg" | JPEG format |
| "png" | PNG format |

### InjectDetails
Used to inject JavaScript or CSS into a page. This type is given as a parameter to tabs.executeScript(), tabs.insertCSS(), and tabs.removeCSS() methods.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| allFrames | boolean | No | false | If true, inject into all frames, even if not the top frame |
| code | string | No* | - | JavaScript or CSS code to inject |
| file | string | No* | - | Path to a file containing code to inject |
| frameId | integer | No | 0 | The frame to inject into (0 is top frame) |
| matchAboutBlank | boolean | No | false | If true, inject into about:blank and about:srcdoc frames |
| runAt | RunAt | No | "document_idle" | When to inject the script |
| cssOrigin | CSSOrigin | No | "author" | The origin of the CSS to inject (CSS only) |

*Note: Either code or file must be specified, but not both

### RunAt
The soonest that the JavaScript or CSS will be injected into the tab.

| Value | Description |
|-------|-------------|
| "document_start" | Corresponds to loading. The DOM is still loading |
| "document_end" | Corresponds to interactive. The DOM has finished loading, but resources may still be loading |
| "document_idle" | Corresponds to complete. The document and all resources have finished loading |

### CSSOrigin
Indicates whether a CSS stylesheet injected by tabs.insertCSS should be treated as an "author" or "user" stylesheet.

| Value | Description |
|-------|-------------|
| "user" | Add CSS as a user stylesheet |
| "author" | Add CSS as an author stylesheet |

## Methods
None (this API only provides types)

## Events
None (this API only provides types)

## Code Examples
These types are typically used with other APIs:

```javascript
// Using ImageDetails with tabs.captureVisibleTab
browser.tabs.captureVisibleTab(null, {
  format: "jpeg",
  quality: 85,
  rect: {
    x: 0,
    y: 0,
    width: 800,
    height: 600
  }
}).then((dataUrl) => {
  console.log("Captured image:", dataUrl);
});

// Using InjectDetails with tabs.executeScript
browser.tabs.executeScript({
  code: 'document.body.style.backgroundColor = "red";',
  allFrames: true,
  runAt: "document_idle"
});

// Using InjectDetails with tabs.insertCSS
browser.tabs.insertCSS({
  file: "content-styles.css",
  allFrames: false,
  cssOrigin: "author"
});
```

## Related APIs
- `tabs` - Uses these types for executeScript(), insertCSS(), and captureVisibleTab()
- `scripting` - The Manifest V3 API that uses similar concepts