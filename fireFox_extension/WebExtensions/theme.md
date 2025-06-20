# theme

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/theme
- **Version**: Current (as of June 2025)

## Overview

Enables browser extensions to get details of the browser's theme and update the theme. You can use this API to include a dynamic theme in your extension, which you define as a `theme.Theme` object and apply using `theme.update()`. 

You cannot include a static theme in your extension using this API. Static themes are defined with the `"theme"` manifest key and are used for themes that don't change dynamically. This API is specifically for extensions that need to programmatically modify the browser's appearance.

## Permissions

To use this API, request the `"theme"` permission in your manifest.json file:

```json
{
  "permissions": ["theme"]
}
```

## Types

### Theme
Represents the content of a theme. This is an object that can contain the following properties:

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| colors | object | No | - | Colors for various UI elements |
| images | object | No | - | Images used in the theme |
| properties | object | No | - | Additional theme properties |

#### Colors Object Properties
| Property | Type | Description |
|----------|------|-------------|
| frame | string | Background color of the header area |
| tab_background_text | string | Text color for the tab area |
| toolbar | string | Background color of the toolbar |
| toolbar_text | string | Text color for toolbar elements |
| toolbar_field | string | Background color of toolbar input fields |
| toolbar_field_text | string | Text color of toolbar input fields |
| toolbar_field_border | string | Border color of toolbar input fields |
| tab_selected | string | Background color of the active tab |
| tab_line | string | Color of the active tab line |
| popup | string | Background color of popups |
| popup_text | string | Text color in popups |
| popup_border | string | Border color of popups |

#### Images Object Properties
| Property | Type | Description |
|----------|------|-------------|
| theme_frame | string | URL to header background image |
| additional_backgrounds | string[] | URLs to additional background images |

## Methods

### getCurrent()
**Syntax**: `browser.theme.getCurrent(windowId)`

Gets the currently used theme as a Theme object.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | integer | No | - | The ID of a window. If provided, gets theme for that window |

#### Returns
- **Type**: `Promise<Theme>`
- **Description**: A Promise that resolves to a Theme object representing the current theme

#### Code Examples
```javascript
function getStyle(themeInfo) {
  if (themeInfo.colors) {
    console.log(`accent color: ${themeInfo.colors.frame}`);
    console.log(`toolbar: ${themeInfo.colors.toolbar}`);
  }
}

async function getCurrentThemeInfo() {
  const themeInfo = await browser.theme.getCurrent();
  getStyle(themeInfo);
}

getCurrentThemeInfo();
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/theme/getCurrent

### update()
**Syntax**: `browser.theme.update(windowId, theme)`

Updates the browser's theme according to the content of the Theme object.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | integer | No | - | The ID of a window. If provided, theme is applied only to that window |
| theme | Theme | Yes | - | Theme object defining the new theme |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the theme is updated

#### Code Examples
```javascript
const sunTheme = {
  images: {
    theme_frame: "sun.jpg"
  },
  colors: {
    frame: "#CF723F",
    tab_background_text: "#111"
  }
};

browser.theme.update(sunTheme);
```

```javascript
// Apply theme to specific window
const day = {
  images: {
    theme_frame: "sun.jpg"
  },
  colors: {
    frame: "#CF723F",
    tab_background_text: "#111"
  }
};

async function updateThemeForCurrentWindow() {
  let currentWindow = await browser.windows.getLastFocused();
  browser.theme.update(currentWindow.id, day);
}

browser.menus.create({
  id: "set-theme",
  title: "set theme",
  contexts: ["all"]
});

browser.menus.onClicked.addListener(updateThemeForCurrentWindow);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/theme/update

### reset()
**Syntax**: `browser.theme.reset(windowId)`

Removes any theme updates made in a call to `theme.update()`.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| windowId | integer | No | - | The ID of a window. If provided, resets theme only for that window |

#### Returns
- **Type**: `Promise<void>`
- **Description**: A Promise that resolves when the theme is reset

#### Code Examples
```javascript
// Reset theme globally
browser.theme.reset();

// Reset theme for specific window
browser.theme.reset(windowId);
```

## Events

### onUpdated
**Fired when**: The browser theme changes

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| updateInfo | object | Information about the theme update |
| updateInfo.theme | Theme | The new theme |
| updateInfo.windowId | integer | The ID of the window the theme was applied to (if window-specific) |

#### Code Examples
```javascript
browser.theme.onUpdated.addListener((updateInfo) => {
  console.log("Theme updated:", updateInfo.theme);
  if (updateInfo.windowId) {
    console.log(`Applied to window: ${updateInfo.windowId}`);
  } else {
    console.log("Applied globally");
  }
});
```

## Example Themes

### Dark Theme
```javascript
const darkTheme = {
  colors: {
    frame: "#2d2d2d",
    tab_background_text: "#ffffff",
    toolbar: "#353535",
    toolbar_text: "#ffffff",
    toolbar_field: "#404040",
    toolbar_field_text: "#ffffff",
    toolbar_field_border: "#505050"
  }
};

browser.theme.update(darkTheme);
```

### Blue Theme with Background
```javascript
const blueTheme = {
  images: {
    theme_frame: "blue_header.png"
  },
  colors: {
    frame: "#1e3a8a",
    tab_background_text: "#ffffff",
    toolbar: "#2563eb",
    toolbar_text: "#ffffff",
    tab_selected: "#3b82f6"
  }
};

browser.theme.update(blueTheme);
```

### Gradient Theme
```javascript
const gradientTheme = {
  colors: {
    frame: "linear-gradient(90deg, #667eea 0%, #764ba2 100%)",
    tab_background_text: "#ffffff",
    toolbar: "#667eea",
    toolbar_text: "#ffffff"
  }
};

browser.theme.update(gradientTheme);
```

## Notes

- Theme changes are not persistent across browser restarts unless the theme is applied by a constantly running extension
- `theme.getCurrent()` only works with WebExtension themes, not with lightweight themes or built-in themes
- When a theme is reset, the browser returns to the user's default theme setting
- Colors can be specified as hex values, RGB values, or CSS color names
- Images should be optimized for the header area dimensions for best results

## Related APIs
- `browserAction` - For themes that interact with browser toolbar
- `windows` - For applying themes to specific windows
- `runtime` - For managing extension lifecycle and theme persistence
