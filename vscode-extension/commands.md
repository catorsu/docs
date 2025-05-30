## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `commands`

Namespace for dealing with commands. In short, a command is a function with a unique identifier. The function is sometimes also called command handler.

Commands can be added to the editor using the `registerCommand` and `registerTextEditorCommand` functions. Commands can be executed manually or from a UI gesture. Those are:

*   palette - Use the `commands`-section in `package.json` to make a command show in the command palette.
*   keybinding - Use the `keybindings`-section in `package.json` to enable keybindings for your extension.

Commands from other extensions and from the editor itself are accessible to an extension. However, when invoking an editor command not all argument types are supported.

This is a sample that registers a command handler and adds an entry for that command to the palette. First register a command handler with the identifier `extension.sayHello`.

```javascript
commands.registerCommand('extension.sayHello', () => { window.showInformationMessage('Hello World!'); });
```

Second, bind the command identifier to a title under which it will show in the palette (`package.json`).

```json
{ "contributes": { "commands": [ { "command": "extension.sayHello", "title": "Hello World" } ] } }
```

#### Functions

*   **`executeCommand<T>(command: string, ...rest: any[]): Thenable<T>`**
    Executes the command denoted by the given command identifier.

    *   Note 1: When executing an editor command not all types are allowed to be passed as arguments. Allowed are the primitive types string, boolean, number, undefined, and null, as well as `Position`, `Range`, `Uri` and `Location`.
    *   Note 2: There are no restrictions when executing commands that have been contributed by extensions.

    | Parameter        | Description                                                                                                                               |
    | :--------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
    | `command`: string  | Identifier of the command to execute.                                                                                                     |
    | `...rest`: any[] | Parameters passed to the command function.                                                                                                |
    | **Returns**      | **Description**                                                                                                                           |
    | `Thenable<T>`    | A thenable that resolves to the returned value of the given command. Returns `undefined` when the command handler function doesn't return anything. |

*   **`getCommands(filterInternal?: boolean): Thenable<string[]>`**
    Retrieve the list of all available commands. Commands starting with an underscore are treated as internal commands.

    | Parameter             | Description                                                              |
    | :-------------------- | :----------------------------------------------------------------------- |
    | `filterInternal?`: boolean | Set true to not see internal commands (starting with an underscore)      |
    | **Returns**           | **Description**                                                          |
    | `Thenable<string[]>`  | Thenable that resolves to a list of command ids.                         |

*   **`registerCommand(command: string, callback: (args: any[]) => any, thisArg?: any): Disposable`**
    Registers a command that can be invoked via a keyboard shortcut, a menu item, an action, or directly.

    Registering a command with an existing command identifier twice will cause an error.

    | Parameter                        | Description                                                    |
    | :------------------------------- | :------------------------------------------------------------- |
    | `command`: string                | A unique identifier for the command.                           |
    | `callback`: `(args: any[]) => any` | A command handler function.                                    |
    | `thisArg?`: any                  | The `this` context used when invoking the handler function.      |
    | **Returns**                      | **Description**                                                |
    | `Disposable`                     | `Disposable` which unregisters this command on disposal.       |

*   **`registerTextEditorCommand(command: string, callback: (textEditor: TextEditor, edit: TextEditorEdit, args: any[]) => void, thisArg?: any): Disposable`**
    Registers a text editor command that can be invoked via a keyboard shortcut, a menu item, an action, or directly.

    Text editor commands are different from ordinary commands as they only execute when there is an active editor when the command is called. Also, the command handler of an editor command has access to the active editor and to an edit-builder. Note that the edit-builder is only valid while the callback executes.

    | Parameter                                                                               | Description                                                                |
    | :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------- |
    | `command`: string                                                                       | A unique identifier for the command.                                       |
    | `callback`: `(textEditor: TextEditor, edit: TextEditorEdit, args: any[]) => void` | A command handler function with access to an editor and an edit.           |
    | `thisArg?`: any                                                                         | The `this` context used when invoking the handler function.                  |
    | **Returns**                                                                             | **Description**                                                            |
    | `Disposable`                                                                            | `Disposable` which unregisters this command on disposal.                   |
