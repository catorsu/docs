# idle

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/idle
- **Version**: WebExtensions API

## Overview

Find out when the user's system is idle, locked, or active. The idle API allows extensions to detect when the user is not actively using their computer, which can be useful for postponing background tasks, showing notifications, or changing application behavior based on user presence.

## Permissions
- `idle` - required

## Types

### IdleState
String describing the device's idle state.

| Value | Description |
|-------|-------------|
| `"active"` | User is actively interacting with the system |
| `"idle"` | User has not generated input for the detection interval |
| `"locked"` | System is locked or screensaver is active |

## Methods

### queryState()
Returns the current idle state of the system.

**Syntax**: `browser.idle.queryState(detectionIntervalInSeconds)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `detectionIntervalInSeconds` | integer | Yes | - | Seconds of inactivity before considering system idle |

#### Returns
- **Type**: `Promise<IdleState>`
- **Description**: The current idle state: "locked", "idle", or "active"

#### Code Examples
```javascript
function onGot(newState) {
  if (newState === "idle") {
    console.log("Please come back — we miss you!");
  } else if (newState === "active") {
    console.log("Glad to still have you with us!");
  } else if (newState === "locked") {
    console.log("System is locked");
  }
}

// Query state with 15 second threshold
let querying = browser.idle.queryState(15);
querying.then(onGot);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/idle/queryState

### setDetectionInterval()
Sets the interval used to determine when the system is idle for `onStateChanged` events.

**Syntax**: `browser.idle.setDetectionInterval(intervalInSeconds)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `intervalInSeconds` | integer | Yes | - | Detection threshold in seconds (minimum: 15) |

**Notes**:
- Default interval is 60 seconds
- Detection interval is per-extension (doesn't affect other extensions)
- Minimum value is 15 seconds

#### Returns
None (void)

#### Code Examples
```javascript
// Set detection interval to 15 seconds (minimum allowed)
browser.idle.setDetectionInterval(15);

// Set detection interval to 5 minutes
browser.idle.setDetectionInterval(300);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/idle/setDetectionInterval

## Events

### onStateChanged
Fired when the system changes between active, idle, or locked states.

**Syntax**: `browser.idle.onStateChanged.addListener(listener)`

**Listener receives**:
- `newState` (IdleState): The new idle state

**State Transitions**:
- → "locked": Screen is locked or screensaver activates
- → "idle": User hasn't generated input for detection interval
- → "active": User generates input on an idle system

#### Code Examples
```javascript
function handleStateChange(newState) {
  console.log(`New state: ${newState}`);
  
  switch(newState) {
    case "active":
      // Resume normal operations
      resumeBackgroundTasks();
      break;
    case "idle":
      // User is away, maybe reduce resource usage
      pauseNonEssentialTasks();
      break;
    case "locked":
      // System is locked, ensure privacy
      hideConfidentialInfo();
      break;
  }
}

// Add listener
browser.idle.onStateChanged.addListener(handleStateChange);

// Remove listener when no longer needed
// browser.idle.onStateChanged.removeListener(handleStateChange);

// Check if listener is registered
if (browser.idle.onStateChanged.hasListener(handleStateChange)) {
  console.log("State change listener is active");
}
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/idle/onStateChanged

## Usage Examples

### Complete Idle Detection System
```javascript
// Configure idle detection
browser.idle.setDetectionInterval(120); // 2 minutes

// State tracking
let currentState = null;

// Handle state changes
browser.idle.onStateChanged.addListener((newState) => {
  if (currentState !== newState) {
    console.log(`State changed from ${currentState} to ${newState}`);
    currentState = newState;
    
    // Notify other parts of extension
    browser.runtime.sendMessage({
      type: 'idle-state-changed',
      state: newState
    });
  }
});

// Periodic state check
async function checkIdleState() {
  const state = await browser.idle.queryState(60);
  console.log(`Current state (60s threshold): ${state}`);
}

// Check state every 5 minutes
setInterval(checkIdleState, 5 * 60 * 1000);
```

### Smart Notification System
```javascript
// Only show notifications when user is active
async function showSmartNotification(title, message) {
  const state = await browser.idle.queryState(30);
  
  if (state === "active") {
    // User is active, show notification
    browser.notifications.create({
      type: "basic",
      iconUrl: "icon.png",
      title: title,
      message: message
    });
  } else {
    // User is away, queue for later
    queueNotificationForLater(title, message);
  }
}
```

### Resource Management
```javascript
let backgroundTaskInterval = null;

browser.idle.onStateChanged.addListener((newState) => {
  if (newState === "idle" || newState === "locked") {
    // User is away, reduce resource usage
    if (backgroundTaskInterval) {
      clearInterval(backgroundTaskInterval);
      backgroundTaskInterval = null;
    }
  } else if (newState === "active") {
    // User is back, resume tasks
    if (!backgroundTaskInterval) {
      backgroundTaskInterval = setInterval(performBackgroundTask, 10000);
    }
  }
});
```

## Best Practices

1. **Minimum Intervals**: Don't set detection intervals below 15 seconds
2. **Resource Usage**: Use idle detection to pause resource-intensive tasks
3. **Privacy**: Be careful with idle detection in privacy-sensitive contexts
4. **State Transitions**: Always handle all three states (active, idle, locked)
5. **Cleanup**: Remove event listeners when no longer needed

## Related APIs
- `alarms` - Schedule code to run at specific times
- `notifications` - Show system notifications based on idle state
- `runtime` - Send messages about idle state changes