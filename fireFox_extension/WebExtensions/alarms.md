# Alarms

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/alarms
- **Version**: All versions

## Overview
Schedule code to run at a specific time in the future. This is like `Window.setTimeout()` and `Window.setInterval()`, except that those functions don't work with background pages that are loaded on demand.

Alarms do not persist across browser sessions. They are created globally across all contexts of a single extension. For example, an alarm created in a background script will fire onAlarm events in background scripts, options pages, popup pages and extension tabs. The Alarms API is not available in content scripts.

## Permissions
- `alarms` - required

## Types
### Alarm
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| name | string | Yes | - | Name of this alarm. This is the name that was passed into the alarms.create() call that created this alarm |
| scheduledTime | number | Yes | - | Time at which the alarm is scheduled to fire next, in milliseconds past the epoch |
| periodInMinutes | number | No | - | If not null, the alarm is a repeating alarm and will fire again in periodInMinutes minutes |

## Methods
### create()
**Syntax**: `browser.alarms.create(name, alarmInfo)`

Creates a new alarm for the current browser session. An alarm may fire once or multiple times. An alarm is cleared after it fires for the last time.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | No | "" | Optional name to identify this alarm. Defaults to the empty string |
| alarmInfo | object | Yes | - | Object describing when the alarm should fire |
| alarmInfo.when | number | No | - | Time the alarm will fire first, given as milliseconds since the epoch. If specified, don't specify delayInMinutes |
| alarmInfo.delayInMinutes | number | No | - | Time the alarm will fire first, given as minutes from the time the alarm is set. If specified, don't specify when |
| alarmInfo.periodInMinutes | number | No | - | If specified, the alarm will fire again every periodInMinutes after its initial firing |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the alarm has been created

#### Code Examples
No code examples in source documentation

### clear()
**Syntax**: `browser.alarms.clear(name)`

Cancels an alarm, given its name.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | No | "" | The name of the alarm to clear. Defaults to the empty string |

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: Fulfilled with true if the alarm was cleared, false otherwise

#### Code Examples
No code examples in source documentation

### clearAll()
**Syntax**: `browser.alarms.clearAll()`

Clear all scheduled alarms.

#### Parameters
None

#### Returns
- **Type**: `Promise<boolean>`
- **Description**: Fulfilled with true if any alarms were cleared, false otherwise

#### Code Examples
No code examples in source documentation

### get()
**Syntax**: `browser.alarms.get(name)`

Gets an alarm, given its name.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | No | "" | The name of the alarm to get. Defaults to the empty string |

#### Returns
- **Type**: `Promise<Alarm>`
- **Description**: Fulfilled with an Alarm object representing the alarm, or undefined if no alarm with that name exists

#### Code Examples
No code examples in source documentation

### getAll()
**Syntax**: `browser.alarms.getAll()`

Gets all active alarms for the extension.

#### Parameters
None

#### Returns
- **Type**: `Promise<Array<Alarm>>`
- **Description**: Fulfilled with an array of Alarm objects. The array is empty if no alarms are active

#### Code Examples
No code examples in source documentation

## Events
### onAlarm
**Fired when**: Any alarm set by the extension goes off

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| alarm | Alarm | The alarm that fired |

## Related APIs
- `setTimeout()` - For delays in regular JavaScript contexts
- `setInterval()` - For recurring tasks in regular JavaScript contexts