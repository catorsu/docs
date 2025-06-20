# Windows

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/windows
- **Version**: Firefox WebExtensions API

## Overview

Interact with browser windows. You can use this API to get information about open windows and to open, modify, and close windows. You can also listen for window open, close, and activate events.

## Types

### WindowType
The type of browser window.

| Value | Description |
|-------|-------------|
| `"normal"` | Regular browser window |
| `"popup"` | Browser popup window |
| `"panel"` | Panel window (deprecated) |
| `"app"` | App window |
| `"devtools"` | Developer tools window |

### WindowState
The state of the browser window.

| Value | Description |
|-------|-------------|
| `"normal"` | Normal window state |
| `"minimized"` | Window is minimized |
| `"maximized"` | Window is maximized |
| `"fullscreen"` | Window is in fullscreen mode |
| `"docked"` | Window is docked (Chrome OS) |

### Window
Object containing information about a browser window.

| Property | Type | Description |
|----------|------|-------------|
| id | integer | Window identifier |
| focused | boolean | Whether window currently has focus |
| top | integer | Pixel offset from top of screen |
| left | integer | Pixel offset from left of screen |
| width | integer | Width in pixels |
| height | integer | Height in pixels |
| tabs | tabs.Tab[] | Array of tabs in the window |
| incognito | boolean | Whether window is incognito/private |
| type | WindowType | Type of browser window |
| state | WindowState | Current state of window |
| alwaysOnTop | boolean | Whether window is set to always be on top |
| sessionId | string | Session ID used for restoring |

### CreateType
Specifies the type of browser window to create.

| Value | Description |
|-------|-------------|
| `"normal"` | Regular browser window |
| `"popup"` | Popup window |
| `"panel"` | Panel window |

## Constants

### WINDOW_ID_NONE
**Value**: `-1`
The windowId value that represents the absence of a browser window.

### WINDOW_ID_CURRENT
**Value**: `-2`
A value that can be used in place of a windowId in some APIs to represent the current window.

## Methods

### get()
**Syntax**: `windows.get(windowId, getInfo)`

Gets details about a window, given its ID.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| windowId | integer | Yes | ID of the window |
| getInfo | object | No | Additional information to retrieve |
| getInfo.populate | boolean | No | Include tabs array |
| getInfo.windowTypes | WindowType[] | No | Restrict to specific window types |

#### Returns
- **Type**: `Promise<Window>`
- **Description**: Window object with details

#### Code Examples
```javascript
async function getCurrentWindow() {
  const window = await browser.windows.get(browser.windows.WINDOW_ID_CURRENT, {
    populate: true
  });
  console.log("Current window has", window.tabs.length, "tabs");
  return window;
}

// Get specific window by ID
async function getWindowById(windowId) {
  try {
    const window = await browser.windows.get(windowId);
    console.log("Window dimensions:", window.width, "x", window.height);
    return window;
  } catch (error) {
    console.error("Window not found:", error);
  }
}
```

### getCurrent()
**Syntax**: `windows.getCurrent(getInfo)`

Gets the current window.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| getInfo | object | No | Additional information to retrieve |
| getInfo.populate | boolean | No | Include tabs array |
| getInfo.windowTypes | WindowType[] | No | Restrict to specific window types |

#### Returns
- **Type**: `Promise<Window>`
- **Description**: Current window object

#### Code Examples
```javascript
async function logCurrentWindow() {
  const currentWindow = await browser.windows.getCurrent({populate: true});
  console.log("Current window ID:", currentWindow.id);
  console.log("Number of tabs:", currentWindow.tabs.length);
  console.log("Window state:", currentWindow.state);
}
```

### getLastFocused()
**Syntax**: `windows.getLastFocused(getInfo)`

Gets the window that was most recently focused — typically the window 'on top'.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| getInfo | object | No | Additional information to retrieve |

#### Returns
- **Type**: `Promise<Window>`
- **Description**: Last focused window object

#### Code Examples
```javascript
async function focusLastWindow() {
  const lastFocused = await browser.windows.getLastFocused();
  console.log("Last focused window:", lastFocused.id);
  
  // Focus it again if not already focused
  if (!lastFocused.focused) {
    await browser.windows.update(lastFocused.id, {focused: true});
  }
}
```

### getAll()
**Syntax**: `windows.getAll(getInfo)`

Gets all windows.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| getInfo | object | No | Additional information to retrieve |
| getInfo.populate | boolean | No | Include tabs array |
| getInfo.windowTypes | WindowType[] | No | Restrict to specific window types |

#### Returns
- **Type**: `Promise<Window[]>`
- **Description**: Array of all window objects

#### Code Examples
```javascript
async function listAllWindows() {
  const windows = await browser.windows.getAll({populate: true});
  
  windows.forEach((window, index) => {
    console.log(`Window ${index + 1}:`);
    console.log(`  ID: ${window.id}`);
    console.log(`  Type: ${window.type}`);
    console.log(`  State: ${window.state}`);
    console.log(`  Tabs: ${window.tabs.length}`);
    console.log(`  Focused: ${window.focused}`);
  });
  
  return windows;
}

// Get only normal windows
async function getNormalWindows() {
  const normalWindows = await browser.windows.getAll({
    windowTypes: ["normal"]
  });
  return normalWindows;
}
```

### create()
**Syntax**: `windows.create(createData)`

Creates a new window.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| createData | object | No | Window creation options |
| createData.url | string or string[] | No | URL(s) to open in new tabs |
| createData.tabId | integer | No | Existing tab to move to new window |
| createData.left | integer | No | Left position in pixels |
| createData.top | integer | No | Top position in pixels |
| createData.width | integer | No | Width in pixels |
| createData.height | integer | No | Height in pixels |
| createData.focused | boolean | No | Whether window should be focused |
| createData.incognito | boolean | No | Whether to open private window |
| createData.type | CreateType | No | Type of window to create |
| createData.state | WindowState | No | Initial window state |

#### Returns
- **Type**: `Promise<Window>`
- **Description**: Created window object

#### Code Examples
```javascript
// Create a basic new window
async function createNewWindow() {
  const newWindow = await browser.windows.create({
    url: "https://mozilla.org",
    type: "normal",
    focused: true
  });
  console.log("Created window with ID:", newWindow.id);
  return newWindow;
}

// Create a popup window
async function createPopup() {
  const popup = await browser.windows.create({
    url: "popup.html",
    type: "popup",
    width: 400,
    height: 300,
    left: 100,
    top: 100
  });
  return popup;
}

// Create window with multiple tabs
async function createMultiTabWindow() {
  const window = await browser.windows.create({
    url: [
      "https://developer.mozilla.org",
      "https://github.com",
      "https://stackoverflow.com"
    ],
    focused: true
  });
  return window;
}

// Create private/incognito window
async function createPrivateWindow() {
  const privateWindow = await browser.windows.create({
    incognito: true,
    url: "https://mozilla.org"
  });
  return privateWindow;
}
```

### update()
**Syntax**: `windows.update(windowId, updateInfo)`

Updates the properties of a window. Use this to move, resize, and (un)focus a window.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| windowId | integer | Yes | ID of window to update |
| updateInfo | object | Yes | Properties to update |
| updateInfo.left | integer | No | New left position |
| updateInfo.top | integer | No | New top position |
| updateInfo.width | integer | No | New width |
| updateInfo.height | integer | No | New height |
| updateInfo.focused | boolean | No | Whether to focus window |
| updateInfo.drawAttention | boolean | No | Whether to draw attention |
| updateInfo.state | WindowState | No | New window state |

#### Returns
- **Type**: `Promise<Window>`
- **Description**: Updated window object

#### Code Examples
```javascript
// Focus a specific window
async function focusWindow(windowId) {
  const window = await browser.windows.update(windowId, {focused: true});
  return window;
}

// Resize and reposition window
async function resizeWindow(windowId) {
  const window = await browser.windows.update(windowId, {
    left: 100,
    top: 100,
    width: 800,
    height: 600
  });
  return window;
}

// Minimize window
async function minimizeWindow(windowId) {
  const window = await browser.windows.update(windowId, {
    state: "minimized"
  });
  return window;
}

// Maximize window
async function maximizeWindow(windowId) {
  const window = await browser.windows.update(windowId, {
    state: "maximized"
  });
  return window;
}

// Center window on screen
async function centerWindow(windowId) {
  const window = await browser.windows.get(windowId);
  const screen = await browser.system.display.getInfo();
  const primaryDisplay = screen.find(display => display.isPrimary);
  
  const centerX = (primaryDisplay.workArea.width - window.width) / 2;
  const centerY = (primaryDisplay.workArea.height - window.height) / 2;
  
  return await browser.windows.update(windowId, {
    left: Math.round(centerX),
    top: Math.round(centerY)
  });
}
```

### remove()
**Syntax**: `windows.remove(windowId)`

Closes a window, and all its tabs.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| windowId | integer | Yes | ID of window to close |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when window is closed

#### Code Examples
```javascript
// Close specific window
async function closeWindow(windowId) {
  try {
    await browser.windows.remove(windowId);
    console.log("Window closed successfully");
  } catch (error) {
    console.error("Failed to close window:", error);
  }
}

// Close all windows except current
async function closeOtherWindows() {
  const currentWindow = await browser.windows.getCurrent();
  const allWindows = await browser.windows.getAll();
  
  for (const window of allWindows) {
    if (window.id !== currentWindow.id) {
      await browser.windows.remove(window.id);
    }
  }
}
```

## Events

### onCreated
**Fired when**: A window is created

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| window | Window | The created window object |

#### Code Examples
```javascript
browser.windows.onCreated.addListener((window) => {
  console.log("New window created:", window.id);
  console.log("Window type:", window.type);
  console.log("Window has", window.tabs?.length || 0, "tabs");
});
```

### onRemoved
**Fired when**: A window is closed

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| windowId | integer | ID of the closed window |

#### Code Examples
```javascript
browser.windows.onRemoved.addListener((windowId) => {
  console.log("Window closed:", windowId);
  
  // Clean up any data associated with this window
  delete windowData[windowId];
});
```

### onFocusChanged
**Fired when**: The currently focused window changes

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| windowId | integer | ID of newly focused window (WINDOW_ID_NONE if none) |

#### Code Examples
```javascript
browser.windows.onFocusChanged.addListener(async (windowId) => {
  if (windowId === browser.windows.WINDOW_ID_NONE) {
    console.log("No window is focused");
  } else {
    console.log("Window focused:", windowId);
    
    // Get details of focused window
    try {
      const window = await browser.windows.get(windowId);
      console.log("Focused window type:", window.type);
    } catch (error) {
      console.log("Could not get window details");
    }
  }
});
```

### onBoundsChanged
**Fired when**: A window is resized or moved

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| window | Window | The window that changed |

#### Code Examples
```javascript
browser.windows.onBoundsChanged.addListener((window) => {
  console.log("Window bounds changed:", window.id);
  console.log("New position:", window.left, window.top);
  console.log("New size:", window.width, window.height);
  
  // Save window position preferences
  browser.storage.local.set({
    [`window_${window.id}_bounds`]: {
      left: window.left,
      top: window.top,
      width: window.width,
      height: window.height
    }
  });
});
```

## Window Management Examples

### Save and Restore Window State
```javascript
// Save current window state
async function saveWindowState() {
  const windows = await browser.windows.getAll();
  const windowStates = windows.map(window => ({
    id: window.id,
    left: window.left,
    top: window.top,
    width: window.width,
    height: window.height,
    state: window.state,
    focused: window.focused
  }));
  
  await browser.storage.local.set({windowStates});
}

// Restore window positions on startup
async function restoreWindowStates() {
  const {windowStates} = await browser.storage.local.get("windowStates");
  if (!windowStates) return;
  
  for (const state of windowStates) {
    await browser.windows.update(state.id, {
      left: state.left,
      top: state.top,
      width: state.width,
      height: state.height,
      state: state.state
    });
  }
}
```

### Window Organizer
```javascript
// Organize windows in a grid
async function organizeWindows() {
  const windows = await browser.windows.getAll({
    windowTypes: ["normal"]
  });
  
  const screenWidth = 1920; // Get from display API in real implementation
  const screenHeight = 1080;
  
  const cols = Math.ceil(Math.sqrt(windows.length));
  const rows = Math.ceil(windows.length / cols);
  
  const windowWidth = Math.floor(screenWidth / cols);
  const windowHeight = Math.floor(screenHeight / rows);
  
  for (let i = 0; i < windows.length; i++) {
    const col = i % cols;
    const row = Math.floor(i / cols);
    
    await browser.windows.update(windows[i].id, {
      left: col * windowWidth,
      top: row * windowHeight,
      width: windowWidth,
      height: windowHeight,
      state: "normal"
    });
  }
}
```

## Related APIs
- `tabs` - Tab management within windows
- `sessions` - Session management and restoration
- `system.display` - Display information

## Notes
- Based on Chromium's chrome.windows API
- Window IDs are unique within browser session
- Some operations may fail if window is already closed
- Private/incognito windows may have limitations
- Window bounds may be constrained by OS or browser settings
