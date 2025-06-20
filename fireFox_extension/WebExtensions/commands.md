# Commands

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/commands
- **Version**: All versions

## Overview
Listens for the user executing commands registered using the commands manifest.json key. Also provides features to update the shortcut key settings.

Commands are keyboard shortcuts that the user can use to invoke extension features. They are defined in the manifest.json file and can be programmatically managed through this API.

## Permissions
- No special permissions required

## Types
### Command
| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| name | string | Yes | - | The name of the command |
| description | string | No | - | The description of the command |
| shortcut | string | No | - | The shortcut key combination |

## Methods
### getAll()
**Syntax**: `browser.commands.getAll()`

Gets all registered commands for the extension.

#### Parameters
None

#### Returns
- **Type**: `Promise<Array<Command>>`
- **Description**: Fulfilled with an array of Command objects

#### Code Examples
No code examples in source documentation

### openShortcutSettings()
**Syntax**: `browser.commands.openShortcutSettings()`

Opens the Manage Extension Shortcuts page, highlighting the extension's shortcut options, if it has any.

#### Parameters
None

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the shortcuts page is opened

#### Code Examples
No code examples in source documentation

### reset()
**Syntax**: `browser.commands.reset(name)`

Resets a command's description and shortcut to the values given in the manifest key.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| name | string | Yes | - | The name of the command to reset |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the command has been reset

#### Code Examples
```javascript
const commandName = "my-command";

function resetShortcut() {
  browser.commands.reset(commandName);
}

document.querySelector("#reset").addEventListener("click", resetShortcut);
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/commands/reset

### update()
**Syntax**: `browser.commands.update(detail)`

Changes the description or shortcut for a command.

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| detail | object | Yes | - | The details of the update |
| detail.name | string | Yes | - | The name of the command to update |
| detail.description | string | No | - | The new description for the command |
| detail.shortcut | string | No | - | The new shortcut for the command |

#### Returns
- **Type**: `Promise<void>`
- **Description**: Fulfilled when the command has been updated

#### Code Examples
No code examples in source documentation

## Events
### onChanged
**Fired when**: The keyboard shortcut for a command is changed

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| changeInfo | object | Object containing information about the change |
| changeInfo.name | string | The name of the command |
| changeInfo.newShortcut | string | The new shortcut |
| changeInfo.oldShortcut | string | The old shortcut |

### onCommand
**Fired when**: A command is executed using its associated keyboard shortcut

#### Listener Parameters
| Name | Type | Description |
|------|------|-------------|
| command | string | The name of the command that was executed |
| tab | tabs.Tab | The active tab when the command was triggered (optional) |

#### Code Examples
In manifest.json:
```json
"commands": {
  "toggle-feature": {
    "suggested_key": {
      "default": "Ctrl+Shift+Y"
    },
    "description": "Send a 'toggle-feature' event"
  }
}
```

In background script:
```javascript
browser.commands.onCommand.addListener((command) => {
  if (command === "toggle-feature") {
    console.log("Toggling the feature!");
  }
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/commands/onCommand

## Manifest Keys
Commands are defined in manifest.json:
```json
{
  "commands": {
    "command-name": {
      "suggested_key": {
        "default": "Ctrl+Shift+Y",
        "mac": "Command+Shift+Y"
      },
      "description": "Description of the command"
    }
  }
}
```

### Special Commands
- `_execute_action` - Triggers the action (toolbar button) click
- `_execute_browser_action` - Triggers the browser action (Manifest V2)
- `_execute_sidebar_action` - Opens the sidebar

### Key Format
- Modifier (required): "Ctrl", "Alt", "Command", or "MacCtrl"
- Secondary modifier (optional): "Shift" or another modifier
- Key: A-Z, 0-9, F1-F19, or special keys

## Related APIs
- `action` - For toolbar button actions
- `browserAction` - For toolbar button actions (Manifest V2)
- `sidebarAction` - For sidebar actions