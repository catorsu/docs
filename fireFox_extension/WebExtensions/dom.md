# DOM

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/dom
- **Version**: Firefox 63+

## Overview
Access special extension-only DOM features. Currently provides access to open or closed shadow roots that would otherwise be inaccessible to extension content scripts.

## Permissions
- No special permissions required

## Types
None

## Methods
### openOrClosedShadowRoot()
**Syntax**: `browser.dom.openOrClosedShadowRoot(element)`

Gets the open shadow root or the closed shadow root hosted by the specified element. If the shadow root isn't attached to the element, it will return null.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| element | Element | Yes | - | The host element of the shadow root |

#### Returns
- **Type**: `ShadowRoot` or `null`
- **Description**: The shadow root hosted by the element, or null if none exists

#### Code Examples
```javascript
// In a content script
const element = document.querySelector('#shadow-host');
const shadowRoot = browser.dom.openOrClosedShadowRoot(element);

if (shadowRoot) {
  // Access shadow DOM content
  const shadowContent = shadowRoot.querySelector('.shadow-element');
}
```

## Events
None

## Related APIs
- Content scripts - Where this API is typically used
- `tabs.executeScript()` - For injecting scripts that can use this API