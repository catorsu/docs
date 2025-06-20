# notifications

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/notifications
- **Version**: WebExtensions API

## Overview

Display notifications to the user, using the underlying operating system's notification mechanism. Because this API uses the operating system's notification mechanism, the details of how notifications appear and behave may differ according to the operating system and the user's settings.

**Platform Differences**:
- **macOS**: Notifications appear in the notification center
- **Windows**: Notifications persist in the Action Center until the browser is closed
- **Linux**: Appearance depends on the desktop environment

## Permissions
- `notifications` - required

## Types

### TemplateType
The type of notification. Determines what content the notification can contain.

| Value | Description | Firefox Support |
|-------|-------------|-----------------|
| `"basic"` | Simple notification with icon, title, and message | ✓ Supported |
| `"image"` | Includes a preview image | ✗ Not supported |
| `"list"` | Contains a list of items | ✗ Not supported |
| `"progress"` | Shows a progress indicator | ✗ Not supported |

**Note**: Firefox currently only supports "basic" notifications.

### NotificationOptions
Defines the content and behavior of a notification.

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `type` | TemplateType | Yes* | - | Type of notification |
| `iconUrl` | string | Yes* | - | URL of icon (data:, blob:, http(s):, or relative) |
| `title` | string | Yes* | - | Notification's title |
| `message` | string | Yes* | - | Notification's main content |
| `buttons` | array | No | - | Up to 2 buttons (not supported in Firefox) |
| `contextMessage` | string | No | - | Additional context (not supported in Firefox) |
| `eventTime` | number | No | - | Timestamp for the notification |
| `imageUrl` | string | No** | - | Preview image URL (type must be "image") |
| `items` | array | No** | - | List items (type must be "list") |
| `priority` | integer | No | 0 | Priority from -2 to 2 |
| `progress` | integer | No** | - | Progress 0-100 (type must be "progress") |

*Required for `create()`, optional for `update()`
**Only allowed for specific notification types

**Note**: For SVG images, include width and height attributes (e.g., `<svg width="96" height="96"...>`)

## Methods

### create()
Creates and displays a new notification.

**Syntax**: `browser.notifications.create(id, options)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `id` | string | No | auto-generated | Unique notification ID |
| `options` | NotificationOptions | Yes | - | Notification content and behavior |

**Warning**: Calling `create()` multiple times in rapid succession may result in no notifications being displayed.

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with the notification ID when display process starts

#### Code Examples
```javascript
// Basic notification
browser.notifications.create({
  type: "basic",
  iconUrl: browser.runtime.getURL("icons/icon-48.png"),
  title: "Notification Title",
  message: "This is the notification message"
});

// Notification with ID
browser.notifications.create("my-notification", {
  type: "basic",
  iconUrl: "icon.png",
  title: "Download complete",
  message: "Your file has been downloaded successfully"
});

// Using data URLs for icons
const canvas = document.createElement('canvas');
// ... draw on canvas ...
browser.notifications.create({
  type: "basic",
  iconUrl: canvas.toDataURL(),
  title: "Dynamic Icon",
  message: "Notification with generated icon"
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/notifications/create

### clear()
Clears a notification, given its ID.

**Syntax**: `browser.notifications.clear(id)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `id` | string | Yes | The notification ID to clear |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: `true` if cleared, `false` if not found

#### Code Examples
```javascript
browser.notifications.clear("my-notification").then((wasCleared) => {
  console.log(wasCleared ? "Notification cleared" : "Notification not found");
});
```

### update()
Updates an existing notification.

**Syntax**: `browser.notifications.update(id, options)`

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `id` | string | Yes | The notification ID to update |
| `options` | NotificationOptions | Yes | Properties to update |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: `true` if updated, `false` if not found

#### Code Examples
```javascript
// Update notification message
browser.notifications.update("my-notification", {
  message: "Updated message content"
});

// Progress notification (if supported)
let progress = 0;
const updateProgress = () => {
  progress += 10;
  browser.notifications.update("download-notification", {
    progress: progress,
    message: `Downloading: ${progress}%`
  });
};
```

### getAll()
Gets all notifications created by this extension.

**Syntax**: `browser.notifications.getAll()`

#### Returns
- **Type**: `Promise<object>`
- **Description**: Object with notification IDs as keys and NotificationOptions as values

#### Code Examples
```javascript
browser.notifications.getAll().then((notifications) => {
  console.log("Active notifications:", Object.keys(notifications).length);
  for (const [id, notification] of Object.entries(notifications)) {
    console.log(`${id}: ${notification.title}`);
  }
});
```

## Events

### onClicked
Fired when the user clicks the notification (but not on a button).

**Syntax**: `browser.notifications.onClicked.addListener(listener)`

**Listener receives**:
- `notificationId` (string): The ID of the clicked notification

#### Code Examples
```javascript
browser.notifications.onClicked.addListener((notificationId) => {
  console.log(`Notification ${notificationId} was clicked`);
  // Open relevant page or perform action
  browser.tabs.create({ url: "https://example.com" });
  // Clear the notification
  browser.notifications.clear(notificationId);
});
```

### onButtonClicked
Fired when the user clicks a button in the notification.

**Syntax**: `browser.notifications.onButtonClicked.addListener(listener)`

**Listener receives**:
- `notificationId` (string): The ID of the notification
- `buttonIndex` (integer): Index of the clicked button (0 or 1)

**Note**: Not supported in Firefox as buttons are not supported

### onClosed
Fired when a notification is closed, either by the system or user.

**Syntax**: `browser.notifications.onClosed.addListener(listener)`

**Listener receives**:
- `notificationId` (string): The ID of the closed notification
- `byUser` (boolean): `true` if closed by user, `false` if by system

#### Code Examples
```javascript
browser.notifications.onClosed.addListener((notificationId, byUser) => {
  console.log(`Notification ${notificationId} closed`);
  console.log(byUser ? "Closed by user" : "Closed by system");
});
```

### onShown
Fired immediately after a notification is shown.

**Syntax**: `browser.notifications.onShown.addListener(listener)`

**Listener receives**:
- `notificationId` (string): The ID of the shown notification

## Usage Examples

### Toggle Notification System
```javascript
let myNotification = "my-notification";

function toggleNotification() {
  browser.notifications.getAll().then((all) => {
    if (myNotification in all) {
      // Clear existing notification
      browser.notifications.clear(myNotification);
    } else {
      // Create new notification
      browser.notifications.create(myNotification, {
        type: "basic",
        iconUrl: browser.runtime.getURL("icons/icon-48.png"),
        title: "Toggle Notification",
        message: "Click again to dismiss"
      });
    }
  });
}

browser.browserAction.onClicked.addListener(toggleNotification);
```

### Notification with Timer
```javascript
// Show notification that auto-dismisses after 5 seconds
function showTimedNotification(title, message) {
  const id = `timed-${Date.now()}`;
  
  browser.notifications.create(id, {
    type: "basic",
    iconUrl: "icon.png",
    title: title,
    message: message
  });
  
  setTimeout(() => {
    browser.notifications.clear(id);
  }, 5000);
}
```

### Download Progress Notification
```javascript
// Simulate download with progress updates
function simulateDownload() {
  const notificationId = "download-progress";
  let progress = 0;
  
  // Create initial notification
  browser.notifications.create(notificationId, {
    type: "basic",
    iconUrl: "download-icon.png",
    title: "Downloading file...",
    message: "Starting download..."
  });
  
  // Update progress
  const interval = setInterval(() => {
    progress += 10;
    
    if (progress > 100) {
      clearInterval(interval);
      browser.notifications.update(notificationId, {
        title: "Download complete!",
        message: "Your file has been downloaded."
      });
      
      // Auto-clear after 3 seconds
      setTimeout(() => {
        browser.notifications.clear(notificationId);
      }, 3000);
    } else {
      browser.notifications.update(notificationId, {
        message: `Progress: ${progress}%`
      });
    }
  }, 500);
}
```

### Context-Aware Notifications
```javascript
// Show different notifications based on context
browser.runtime.onMessage.addListener((message) => {
  const baseOptions = {
    type: "basic",
    iconUrl: "icon.png"
  };
  
  switch (message.type) {
    case "success":
      browser.notifications.create({
        ...baseOptions,
        title: "Success!",
        message: message.text,
        iconUrl: "success-icon.png"
      });
      break;
      
    case "error":
      browser.notifications.create({
        ...baseOptions,
        title: "Error",
        message: message.text,
        iconUrl: "error-icon.png"
      });
      break;
      
    case "info":
      browser.notifications.create({
        ...baseOptions,
        title: "Information",
        message: message.text
      });
      break;
  }
});
```

## Best Practices

1. **Avoid Spam**: Don't create notifications too frequently
2. **Use Clear IDs**: Use meaningful IDs for easy management
3. **Handle Events**: Always handle click events to provide functionality
4. **Auto-dismiss**: Consider auto-dismissing non-critical notifications
5. **Icon Requirements**: Use appropriate icon sizes (typically 48x48 or 96x96)
6. **Test Cross-platform**: Test on different operating systems

## Firefox Limitations

1. Only supports "basic" notification type
2. No support for buttons, lists, or progress indicators
3. No support for image previews
4. Limited styling options

## Related APIs
- `alarms` - Schedule notifications at specific times
- `runtime` - Send messages when notifications are clicked
- `tabs` - Open tabs in response to notification clicks
- `browserAction` - Trigger notifications from toolbar button