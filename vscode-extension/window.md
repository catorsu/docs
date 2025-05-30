## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `window`

Namespace for dealing with the current window of the editor. That is visible and active editors, as well as, UI elements to show messages, selections, and asking for user input.

#### Variables

*   **`activeColorTheme`**: `ColorTheme`
    The currently active color theme as configured in the settings. The active theme can be changed via the `workbench.colorTheme` setting.
*   **`activeNotebookEditor`**: `NotebookEditor | undefined`
    The currently active notebook editor or `undefined`. The active editor is the one that currently has focus or, when none has focus, the one that has changed input most recently.
*   **`activeTerminal`**: `Terminal | undefined`
    The currently active terminal or `undefined`. The active terminal is the one that currently has focus or most recently had focus.
*   **`activeTextEditor`**: `TextEditor | undefined`
    The currently active editor or `undefined`. The active editor is the one that currently has focus or, when none has focus, the one that has changed input most recently.
*   **`state`**: `WindowState`
    Represents the current window's state.
*   **`tabGroups`**: `TabGroups`
    Represents the grid widget within the main editor area
*   **`terminals`**: `readonly Terminal[]`
    The currently opened terminals or an empty array.
*   **`visibleNotebookEditors`**: `readonly NotebookEditor[]`
    The currently visible notebook editors or an empty array.
*   **`visibleTextEditors`**: `readonly TextEditor[]`
    The currently visible editors or an empty array.

#### Events

*   **`onDidChangeActiveColorTheme`**: `Event<ColorTheme>`
    An Event which fires when the active color theme is changed or has changes.
*   **`onDidChangeActiveNotebookEditor`**: `Event<NotebookEditor | undefined>`
    An Event which fires when the active notebook editor has changed. Note that the event also fires when the active editor changes to `undefined`.
*   **`onDidChangeActiveTerminal`**: `Event<Terminal | undefined>`
    An Event which fires when the active terminal has changed. Note that the event also fires when the active terminal changes to `undefined`.
*   **`onDidChangeActiveTextEditor`**: `Event<TextEditor | undefined>`
    An Event which fires when the active editor has changed. Note that the event also fires when the active editor changes to `undefined`.
*   **`onDidChangeNotebookEditorSelection`**: `Event<NotebookEditorSelectionChangeEvent>`
    An Event which fires when the notebook editor selections have changed.
*   **`onDidChangeNotebookEditorVisibleRanges`**: `Event<NotebookEditorVisibleRangesChangeEvent>`
    An Event which fires when the notebook editor visible ranges have changed.
*   **`onDidChangeTerminalShellIntegration`**: `Event<TerminalShellIntegrationChangeEvent>`
    Fires when shell integration activates or one of its properties changes in a terminal.
*   **`onDidChangeTerminalState`**: `Event<Terminal>`
    An Event which fires when a terminal's state has changed.
*   **`onDidChangeTextEditorOptions`**: `Event<TextEditorOptionsChangeEvent>`
    An Event which fires when the options of an editor have changed.
*   **`onDidChangeTextEditorSelection`**: `Event<TextEditorSelectionChangeEvent>`
    An Event which fires when the selection in an editor has changed.
*   **`onDidChangeTextEditorViewColumn`**: `Event<TextEditorViewColumnChangeEvent>`
    An Event which fires when the view column of an editor has changed.
*   **`onDidChangeTextEditorVisibleRanges`**: `Event<TextEditorVisibleRangesChangeEvent>`
    An Event which fires when the visible ranges of an editor has changed.
*   **`onDidChangeVisibleNotebookEditors`**: `Event<readonly NotebookEditor[]>`
    An Event which fires when the visible notebook editors has changed.
*   **`onDidChangeVisibleTextEditors`**: `Event<readonly TextEditor[]>`
    An Event which fires when the array of visible editors has changed.
*   **`onDidChangeWindowState`**: `Event<WindowState>`
    An Event which fires when the focus or activity state of the current window changes. The value of the event represents whether the window is focused.
*   **`onDidCloseTerminal`**: `Event<Terminal>`
    An Event which fires when a terminal is disposed.
*   **`onDidEndTerminalShellExecution`**: `Event<TerminalShellExecutionEndEvent>`
    This will be fired when a terminal command is ended. This event will fire only when shell integration is activated for the terminal.
*   **`onDidOpenTerminal`**: `Event<Terminal>`
    An Event which fires when a terminal has been created, either through the `createTerminal` API or commands.
*   **`onDidStartTerminalShellExecution`**: `Event<TerminalShellExecutionStartEvent>`
    This will be fired when a terminal command is started. This event will fire only when shell integration is activated for the terminal.

#### Functions

*   **`createInputBox(): InputBox`**
    Creates a `InputBox` to let the user enter some text input.

    Note that in many cases the more convenient `window.showInputBox` is easier to use. `window.createInputBox` should be used when `window.showInputBox` does not offer the required flexibility.

    | Parameter   | Description     |
    | :---------- | :-------------- |
    | **Returns** | **Description** |
    | `InputBox`  | A new `InputBox`. |

*   **`createOutputChannel(name: string, languageId?: string): OutputChannel`**
    Creates a new output channel with the given name and language id If `languageId` is not provided, then `Log` is used as default language id.

    You can access the visible or active output channel as a text document from visible editors or active editor and use the `languageId` to contribute language features like syntax coloring, code lens etc.,

    | Parameter           | Description                                                              |
    | :------------------ | :----------------------------------------------------------------------- |
    | `name`: string      | Human-readable string which will be used to represent the channel in the UI. |
    | `languageId?`: string | The identifier of the language associated with the channel.              |
    | **Returns**         | **Description**                                                          |
    | `OutputChannel`     | A new output channel.                                                    |

*   **`createOutputChannel(name: string, options: {log: true}): LogOutputChannel`**
    Creates a new log output channel with the given name.

    | Parameter                 | Description                                                              |
    | :------------------------ | :----------------------------------------------------------------------- |
    | `name`: string            | Human-readable string which will be used to represent the channel in the UI. |
    | `options`: `{log: true}`  | Options for the log output channel.                                      |
    | **Returns**               | **Description**                                                          |
    | `LogOutputChannel`        | A new log output channel.                                                |

*   **`createQuickPick<T extends QuickPickItem>(): QuickPick<T>`**
    Creates a `QuickPick` to let the user pick an item from a list of items of type T.

    Note that in many cases the more convenient `window.showQuickPick` is easier to use. `window.createQuickPick` should be used when `window.showQuickPick` does not offer the required flexibility.

    | Parameter      | Description       |
    | :------------- | :---------------- |
    | **Returns**    | **Description**   |
    | `QuickPick<T>` | A new `QuickPick`. |

*   **`createStatusBarItem(id: string, alignment?: StatusBarAlignment, priority?: number): StatusBarItem`**
    Creates a status bar item.

    | Parameter                       | Description                                                                          |
    | :------------------------------ | :----------------------------------------------------------------------------------- |
    | `id`: string                    | The identifier of the item. Must be unique within the extension.                     |
    | `alignment?`: `StatusBarAlignment` | The alignment of the item.                                                           |
    | `priority?`: `number`           | The priority of the item. Higher values mean the item should be shown more to the left. |
    | **Returns**                     | **Description**                                                                      |
    | `StatusBarItem`                 | A new status bar item.                                                               |

*   **`createStatusBarItem(alignment?: StatusBarAlignment, priority?: number): StatusBarItem`**
    Creates a status bar item.

    See also `createStatusBarItem` for creating a status bar item with an identifier.

    | Parameter                       | Description                                                                          |
    | :------------------------------ | :----------------------------------------------------------------------------------- |
    | `alignment?`: `StatusBarAlignment` | The alignment of the item.                                                           |
    | `priority?`: `number`           | The priority of the item. Higher values mean the item should be shown more to the left. |
    | **Returns**                     | **Description**                                                                      |
    | `StatusBarItem`                 | A new status bar item.                                                               |

*   **`createTerminal(name?: string, shellPath?: string, shellArgs?: string | readonly string[]): Terminal`**
    Creates a `Terminal` with a backing shell process. The `cwd` of the terminal will be the workspace directory if it exists.
    *   throws - When running in an environment where a new process cannot be started.

    | Parameter                                 | Description                                                                                                |
    | :---------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
    | `name?`: string                           | Optional human-readable string which will be used to represent the terminal in the UI.                     |
    | `shellPath?`: string                      | Optional path to a custom shell executable to be used in the terminal.                                     |
    | `shellArgs?`: string \| `readonly string[]` | Optional args for the custom shell executable. A string can be used on Windows only which allows specifying shell args in command-line format. |
    | **Returns**                               | **Description**                                                                                            |
    | `Terminal`                                | A new `Terminal`.                                                                                          |

*   **`createTerminal(options: TerminalOptions): Terminal`**
    Creates a `Terminal` with a backing shell process.
    *   throws - When running in an environment where a new process cannot be started.

    | Parameter               | Description                                                              |
    | :---------------------- | :----------------------------------------------------------------------- |
    | `options`: `TerminalOptions` | A `TerminalOptions` object describing the characteristics of the new terminal. |
    | **Returns**             | **Description**                                                          |
    | `Terminal`              | A new `Terminal`.                                                        |

*   **`createTerminal(options: ExtensionTerminalOptions): Terminal`**
    Creates a `Terminal` where an extension controls its input and output.

    | Parameter                            | Description                                                                      |
    | :----------------------------------- | :------------------------------------------------------------------------------- |
    | `options`: `ExtensionTerminalOptions` | An `ExtensionTerminalOptions` object describing the characteristics of the new terminal. |
    | **Returns**                          | **Description**                                                                  |
    | `Terminal`                           | A new `Terminal`.                                                                |

*   **`createTextEditorDecorationType(options: DecorationRenderOptions): TextEditorDecorationType`**
    Create a `TextEditorDecorationType` that can be used to add decorations to text editors.

    | Parameter                             | Description                                  |
    | :------------------------------------ | :------------------------------------------- |
    | `options`: `DecorationRenderOptions`  | Rendering options for the decoration type.   |
    | **Returns**                           | **Description**                              |
    | `TextEditorDecorationType`            | A new decoration type instance.              |

*   **`createTreeView<T>(viewId: string, options: TreeViewOptions<T>): TreeView<T>`**
    Create a `TreeView` for the view contributed using the extension point `views`.

    | Parameter                         | Description                                                        |
    | :-------------------------------- | :----------------------------------------------------------------- |
    | `viewId`: string                  | Id of the view contributed using the extension point `views`.      |
    | `options`: `TreeViewOptions<T>`   | Options for creating the `TreeView`                                |
    | **Returns**                       | **Description**                                                    |
    | `TreeView<T>`                     | a `TreeView`.                                                      |

*   **`createWebviewPanel(viewType: string, title: string, showOptions: ViewColumn | {preserveFocus: boolean, viewColumn: ViewColumn}, options?: WebviewPanelOptions & WebviewOptions): WebviewPanel`**
    Create and show a new webview panel.

    | Parameter                                                                                             | Description                                                                                                |
    | :---------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
    | `viewType`: string                                                                                    | Identifies the type of the webview panel.                                                                  |
    | `title`: string                                                                                       | Title of the panel.                                                                                        |
    | `showOptions`: `ViewColumn` \| {`preserveFocus`: `boolean`, `viewColumn`: `ViewColumn`}               | Where to show the webview in the editor. If `preserveFocus` is set, the new webview will not take focus. |
    | `options?`: `WebviewPanelOptions` & `WebviewOptions`                                                  | Settings for the new panel.                                                                                |
    | **Returns**                                                                                           | **Description**                                                                                            |
    | `WebviewPanel`                                                                                        | New webview panel.                                                                                         |

*   **`registerCustomEditorProvider(viewType: string, provider: CustomTextEditorProvider | CustomReadonlyEditorProvider<CustomDocument> | CustomEditorProvider<CustomDocument>, options?: {supportsMultipleEditorsPerDocument: boolean, webviewOptions: WebviewPanelOptions}): Disposable`**
    Register a provider for custom editors for the `viewType` contributed by the `customEditors` extension point.

    When a custom editor is opened, an `onCustomEditor:viewType` activation event is fired. Your extension must register a `CustomTextEditorProvider`, `CustomReadonlyEditorProvider`, `CustomEditorProvider`for `viewType` as part of activation.

    | Parameter                                                                                                                                                           | Description                                                                                                                            |
    | :------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------- |
    | `viewType`: string                                                                                                                                                  | Unique identifier for the custom editor provider. This should match the `viewType` from the `customEditors` contribution point.        |
    | `provider`: `CustomTextEditorProvider` \| `CustomReadonlyEditorProvider<CustomDocument>` \| `CustomEditorProvider<CustomDocument>`                                    | Provider that resolves custom editors.                                                                                                 |
    | `options?`: {`supportsMultipleEditorsPerDocument`: `boolean`, `webviewOptions`: `WebviewPanelOptions`}                                                                | Options for the provider.                                                                                                              |
    | **Returns**                                                                                                                                                         | **Description**                                                                                                                        |
    | `Disposable`                                                                                                                                                        | `Disposable` that unregisters the provider.                                                                                            |

*   **`registerFileDecorationProvider(provider: FileDecorationProvider): Disposable`**
    Register a file decoration provider.

    | Parameter                         | Description                                                        |
    | :-------------------------------- | :----------------------------------------------------------------- |
    | `provider`: `FileDecorationProvider` | A `FileDecorationProvider`.                                        |
    | **Returns**                       | **Description**                                                    |
    | `Disposable`                      | A `Disposable` that unregisters the provider.                      |

*   **`registerTerminalLinkProvider(provider: TerminalLinkProvider<TerminalLink>): Disposable`**
    Register provider that enables the detection and handling of links within the terminal.

    | Parameter                                           | Description                                                        |
    | :-------------------------------------------------- | :----------------------------------------------------------------- |
    | `provider`: `TerminalLinkProvider<TerminalLink>`    | The provider that provides the terminal links.                     |
    | **Returns**                                         | **Description**                                                    |
    | `Disposable`                                        | `Disposable` that unregisters the provider.                        |

*   **`registerTerminalProfileProvider(id: string, provider: TerminalProfileProvider): Disposable`**
    Registers a provider for a contributed terminal profile.

    | Parameter                             | Description                                                        |
    | :------------------------------------ | :----------------------------------------------------------------- |
    | `id`: string                          | The ID of the contributed terminal profile.                        |
    | `provider`: `TerminalProfileProvider` | The terminal profile provider.                                     |
    | **Returns**                           | **Description**                                                    |
    | `Disposable`                          | A `Disposable` that unregisters the provider.                      |

*   **`registerTreeDataProvider<T>(viewId: string, treeDataProvider: TreeDataProvider<T>): Disposable`**
    Register a `TreeDataProvider` for the view contributed using the extension point `views`. This will allow you to contribute data to the `TreeView` and update if the data changes.

    Note: To get access to the `TreeView` and perform operations on it, use `createTreeView`.

    | Parameter                               | Description                                                              |
    | :-------------------------------------- | :----------------------------------------------------------------------- |
    | `viewId`: string                        | Id of the view contributed using the extension point `views`.            |
    | `treeDataProvider`: `TreeDataProvider<T>` | A `TreeDataProvider` that provides tree data for the view                |
    | **Returns**                             | **Description**                                                          |
    | `Disposable`                            | A `Disposable` that unregisters the `TreeDataProvider`.                  |

*   **`registerUriHandler(handler: UriHandler): Disposable`**
    Registers a `Uri` handler capable of handling system-wide uris. In case there are multiple windows open, the topmost window will handle the `Uri`. A `Uri` handler is scoped to the extension it is contributed from; it will only be able to handle uris which are directed to the extension itself. A `Uri` must respect the following rules:
    *   The `Uri`-scheme must be `vscode.env.uriScheme`;
    *   The `Uri`-authority must be the extension id (e.g. `my.extension`);
    *   The `Uri`-path, -query and -fragment parts are arbitrary.

    For example, if the `my.extension` extension registers a `Uri` handler, it will only be allowed to handle uris with the prefix `product-name://my.extension`.

    An extension can only register a single `Uri` handler in its entire activation lifetime.
    *   Note: There is an activation event `onUri` that fires when a `Uri` directed for the current extension is about to be handled.

    | Parameter             | Description                                                        |
    | :-------------------- | :----------------------------------------------------------------- |
    | `handler`: `UriHandler` | The `Uri` handler to register for this extension.                  |
    | **Returns**           | **Description**                                                    |
    | `Disposable`          | A `Disposable` that unregisters the handler.                       |

*   **`registerWebviewPanelSerializer(viewType: string, serializer: WebviewPanelSerializer<unknown>): Disposable`**
    Registers a webview panel serializer.

    Extensions that support reviving should have an `\"onWebviewPanel:viewType\"` activation event and make sure that `registerWebviewPanelSerializer` is called during activation.

    Only a single serializer may be registered at a time for a given `viewType`.

    | Parameter                                       | Description                                                        |
    | :---------------------------------------------- | :----------------------------------------------------------------- |
    | `viewType`: string                              | Type of the webview panel that can be serialized.                  |
    | `serializer`: `WebviewPanelSerializer<unknown>` | Webview serializer.                                                |
    | **Returns**                                     | **Description**                                                    |
    | `Disposable`                                    | A `Disposable` that unregisters the serializer.                    |

*   **`registerWebviewViewProvider(viewId: string, provider: WebviewViewProvider, options?: {webviewOptions: {retainContextWhenHidden: boolean}}): Disposable`**
    Register a new provider for webview views.

    | Parameter                                                               | Description                                                                                                |
    | :---------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
    | `viewId`: string                                                        | Unique id of the view. This should match the id from the `views` contribution in the `package.json`.       |
    | `provider`: `WebviewViewProvider`                                       | Provider for the webview views.                                                                            |
    | `options?`: {`webviewOptions`: {`retainContextWhenHidden`: `boolean`}} |                                                                                                            |
    | **Returns**                                                             | **Description**                                                                                            |
    | `Disposable`                                                            | `Disposable` that unregisters the provider.                                                                |

*   **`setStatusBarMessage(text: string, hideAfterTimeout: number): Disposable`**
    Set a message to the status bar. This is a short hand for the more powerful status bar items.

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `text`: string            | The message to show, supports icon substitution as in status bar items.              |
    | `hideAfterTimeout`: `number` | Timeout in milliseconds after which the message will be disposed.                    |
    | **Returns**               | **Description**                                                                      |
    | `Disposable`              | A `Disposable` which hides the status bar message.                                   |

*   **`setStatusBarMessage(text: string, hideWhenDone: Thenable<any>): Disposable`**
    Set a message to the status bar. This is a short hand for the more powerful status bar items.

    | Parameter                   | Description                                                                          |
    | :-------------------------- | :----------------------------------------------------------------------------------- |
    | `text`: string              | The message to show, supports icon substitution as in status bar items.              |
    | `hideWhenDone`: `Thenable<any>` | Thenable on which completion (resolve or reject) the message will be disposed.       |
    | **Returns**                 | **Description**                                                                      |
    | `Disposable`                | A `Disposable` which hides the status bar message.                                   |

*   **`setStatusBarMessage(text: string): Disposable`**
    Set a message to the status bar. This is a short hand for the more powerful status bar items.

    Note that status bar messages stack and that they must be disposed when no longer used.

    | Parameter     | Description                                                                          |
    | :------------ | :----------------------------------------------------------------------------------- |
    | `text`: string  | The message to show, supports icon substitution as in status bar items.              |
    | **Returns**   | **Description**                                                                      |
    | `Disposable`  | A `Disposable` which hides the status bar message.                                   |

*   **`showErrorMessage<T extends string>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show an error message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showErrorMessage<T extends string>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show an error message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showErrorMessage<T extends MessageItem>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show an error message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showErrorMessage<T extends MessageItem>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show an error message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showInformationMessage<T extends string>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show an information message to users. Optionally provide an array of items which will be presented as clickable buttons.

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showInformationMessage<T extends string>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show an information message to users. Optionally provide an array of items which will be presented as clickable buttons.

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showInformationMessage<T extends MessageItem>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show an information message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showInformationMessage<T extends MessageItem>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show an information message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showInputBox(options?: InputBoxOptions, token?: CancellationToken): Thenable<string | undefined>`**
    Opens an input box to ask the user for input.

    The returned value will be `undefined` if the input box was canceled (e.g. pressing ESC). Otherwise the returned value will be the string typed by the user or an empty string if the user did not type anything but dismissed the input box with OK.

    | Parameter                       | Description                                                                                                |
    | :------------------------------ | :--------------------------------------------------------------------------------------------------------- |
    | `options?`: `InputBoxOptions`   | Configures the behavior of the input box.                                                                  |
    | `token?`: `CancellationToken`   | A token that can be used to signal cancellation.                                                           |
    | **Returns**                     | **Description**                                                                                            |
    | `Thenable<string | undefined>` | A promise that resolves to a string the user provided or to `undefined` in case of dismissal.              |

*   **`showNotebookDocument(document: NotebookDocument, options?: NotebookDocumentShowOptions): Thenable<NotebookEditor>`**
    Show the given `NotebookDocument` in a notebook editor.

    | Parameter                               | Description                                                                          |
    | :-------------------------------------- | :----------------------------------------------------------------------------------- |
    | `document`: `NotebookDocument`          | A text document to be shown.                                                         |
    | `options?`: `NotebookDocumentShowOptions` | Editor options to configure the behavior of showing the notebook editor.             |
    | **Returns**                             | **Description**                                                                      |
    | `Thenable<NotebookEditor>`              | A promise that resolves to an notebook editor.                                       |

*   **`showOpenDialog(options?: OpenDialogOptions): Thenable<Uri[] | undefined>`**
    Shows a file open dialog to the user which allows to select a file for opening-purposes.

    | Parameter                     | Description                                                                          |
    | :---------------------------- | :----------------------------------------------------------------------------------- |
    | `options?`: `OpenDialogOptions` | Options that control the dialog.                                                     |
    | **Returns**                   | **Description**                                                                      |
    | `Thenable<Uri[] | undefined>` | A promise that resolves to the selected resources or `undefined`.                    |

*   **`showQuickPick(items: readonly string[] | Thenable<readonly string[]>, options: QuickPickOptions & {canPickMany: true}, token?: CancellationToken): Thenable<string[] | undefined>`**
    Shows a selection list allowing multiple selections.

    | Parameter                                                                 | Description                                                                          |
    | :------------------------------------------------------------------------ | :----------------------------------------------------------------------------------- |
    | `items`: `readonly string[]` \| `Thenable<readonly string[]>`             | An array of strings, or a promise that resolves to an array of strings.              |
    | `options`: `QuickPickOptions` & {`canPickMany`: `true`}                   | Configures the behavior of the selection list.                                       |
    | `token?`: `CancellationToken`                                             | A token that can be used to signal cancellation.                                     |
    | **Returns**                                                               | **Description**                                                                      |
    | `Thenable<string[] | undefined>`                                          | A promise that resolves to the selected items or `undefined`.                        |

*   **`showQuickPick(items: readonly string[] | Thenable<readonly string[]>, options?: QuickPickOptions, token?: CancellationToken): Thenable<string | undefined>`**
    Shows a selection list.

    | Parameter                                                                 | Description                                                                          |
    | :------------------------------------------------------------------------ | :----------------------------------------------------------------------------------- |
    | `items`: `readonly string[]` \| `Thenable<readonly string[]>`             | An array of strings, or a promise that resolves to an array of strings.              |
    | `options?`: `QuickPickOptions`                                            | Configures the behavior of the selection list.                                       |
    | `token?`: `CancellationToken`                                             | A token that can be used to signal cancellation.                                     |
    | **Returns**                                                               | **Description**                                                                      |
    | `Thenable<string | undefined>`                                            | A promise that resolves to the selection or `undefined`.                             |

*   **`showQuickPick<T extends QuickPickItem>(items: readonly T[] | Thenable<readonly T[]>, options: QuickPickOptions & {canPickMany: true}, token?: CancellationToken): Thenable<T[] | undefined>`**
    Shows a selection list allowing multiple selections.

    | Parameter                                                                 | Description                                                                          |
    | :------------------------------------------------------------------------ | :----------------------------------------------------------------------------------- |
    | `items`: `readonly T[]` \| `Thenable<readonly T[]>`                       | An array of items, or a promise that resolves to an array of items.                  |
    | `options`: `QuickPickOptions` & {`canPickMany`: `true`}                   | Configures the behavior of the selection list.                                       |
    | `token?`: `CancellationToken`                                             | A token that can be used to signal cancellation.                                     |
    | **Returns**                                                               | **Description**                                                                      |
    | `Thenable<T[] | undefined>`                                              | A promise that resolves to the selected items or `undefined`.                        |

*   **`showQuickPick<T extends QuickPickItem>(items: readonly T[] | Thenable<readonly T[]>, options?: QuickPickOptions, token?: CancellationToken): Thenable<T | undefined>`**
    Shows a selection list.

    | Parameter                                                                 | Description                                                                          |
    | :------------------------------------------------------------------------ | :----------------------------------------------------------------------------------- |
    | `items`: `readonly T[]` \| `Thenable<readonly T[]>`                       | An array of items, or a promise that resolves to an array of items.                  |
    | `options?`: `QuickPickOptions`                                            | Configures the behavior of the selection list.                                       |
    | `token?`: `CancellationToken`                                             | A token that can be used to signal cancellation.                                     |
    | **Returns**                                                               | **Description**                                                                      |
    | `Thenable<T | undefined>`                                                | A promise that resolves to the selected item or `undefined`.                         |

*   **`showSaveDialog(options?: SaveDialogOptions): Thenable<Uri | undefined>`**
    Shows a file save dialog to the user which allows to select a file for saving-purposes.

    | Parameter                     | Description                                                                          |
    | :---------------------------- | :----------------------------------------------------------------------------------- |
    | `options?`: `SaveDialogOptions` | Options that control the dialog.                                                     |
    | **Returns**                   | **Description**                                                                      |
    | `Thenable<Uri | undefined>`   | A promise that resolves to the selected resource or `undefined`.                     |

*   **`showTextDocument(document: TextDocument, column?: ViewColumn, preserveFocus?: boolean): Thenable<TextEditor>`**
    Show the given document in a text editor. A column can be provided to control where the editor is being shown. Might change the active editor.

    | Parameter                   | Description                                                                                                                                                                                                                                                        |
    | :-------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `document`: `TextDocument`  | A text document to be shown.                                                                                                                                                                                                                                       |
    | `column?`: `ViewColumn`     | A view column in which the editor should be shown. The default is the active. Columns that do not exist will be created as needed up to the maximum of `ViewColumn.Nine`. Use `ViewColumn.Beside` to open the editor to the side of the currently active one. |
    | `preserveFocus?`: `boolean` | When `true` the editor will not take focus.                                                                                                                                                                                                                          |
    | **Returns**                 | **Description**                                                                                                                                                                                                                                                    |
    | `Thenable<TextEditor>`      | A promise that resolves to an editor.                                                                                                                                                                                                                              |

*   **`showTextDocument(document: TextDocument, options?: TextDocumentShowOptions): Thenable<TextEditor>`**
    Show the given document in a text editor. Options can be provided to control options of the editor is being shown. Might change the active editor.

    | Parameter                             | Description                                                                          |
    | :------------------------------------ | :----------------------------------------------------------------------------------- |
    | `document`: `TextDocument`            | A text document to be shown.                                                         |
    | `options?`: `TextDocumentShowOptions` | Editor options to configure the behavior of showing the editor.                      |
    | **Returns**                           | **Description**                                                                      |
    | `Thenable<TextEditor>`                | A promise that resolves to an editor.                                                |

*   **`showTextDocument(uri: Uri, options?: TextDocumentShowOptions): Thenable<TextEditor>`**
    A short-hand for `openTextDocument(uri).then(document => showTextDocument(document, options))`.

    See also `workspace.openTextDocument`

    | Parameter                             | Description                                                                          |
    | :------------------------------------ | :----------------------------------------------------------------------------------- |
    | `uri`: `Uri`                          | A resource identifier.                                                               |
    | `options?`: `TextDocumentShowOptions` | Editor options to configure the behavior of showing the editor.                      |
    | **Returns**                           | **Description**                                                                      |
    | `Thenable<TextEditor>`                | A promise that resolves to an editor.                                                |

*   **`showWarningMessage<T extends string>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show a warning message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showWarningMessage<T extends string>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show a warning message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showWarningMessage<T extends MessageItem>(message: string, ...items: T[]): Thenable<T | undefined>`**
    Show a warning message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showWarningMessage<T extends MessageItem>(message: string, options: MessageOptions, ...items: T[]): Thenable<T | undefined>`**
    Show a warning message.

    See also `showInformationMessage`

    | Parameter                 | Description                                                                          |
    | :------------------------ | :----------------------------------------------------------------------------------- |
    | `message`: string         | The message to show.                                                                 |
    | `options`: `MessageOptions` | Configures the behaviour of the message.                                             |
    | `...items`: `T[]`         | A set of items that will be rendered as actions in the message.                      |
    | **Returns**               | **Description**                                                                      |
    | `Thenable<T | undefined>` | A thenable that resolves to the selected item or `undefined` when being dismissed.   |

*   **`showWorkspaceFolderPick(options?: WorkspaceFolderPickOptions): Thenable<WorkspaceFolder | undefined>`**
    Shows a selection list of workspace folders to pick from. Returns `undefined` if no folder is open.

    | Parameter                             | Description                                                                          |
    | :------------------------------------ | :----------------------------------------------------------------------------------- |
    | `options?`: `WorkspaceFolderPickOptions` | Configures the behavior of the workspace folder list.                                |
    | **Returns**                           | **Description**                                                                      |
    | `Thenable<WorkspaceFolder | undefined>` | A promise that resolves to the workspace folder or `undefined`.                      |

*   **`withProgress<R>(options: ProgressOptions, task: (progress: Progress<{increment: number, message: string}>, token: CancellationToken) => Thenable<R>): Thenable<R>`**
    Show progress in the editor. Progress is shown while running the given callback and while the promise it returned isn't resolved nor rejected. The location at which progress should show (and other details) is defined via the passed `ProgressOptions`.

    | Parameter                                                                                                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
    | :------------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `options`: `ProgressOptions`                                                                                    | A `ProgressOptions`-object describing the options to use for showing progress, like its location                                                                                                                                                                                                                                                                                                                                                                                               |
    | `task`: (`progress`: `Progress`<{`increment`: number, `message`: string}>, `token`: `CancellationToken`) => `Thenable<R>` | A callback returning a promise. Progress state can be reported with the provided `Progress`-object.  To report discrete progress, use `increment` to indicate how much work has been completed. Each call with a `increment` value will be summed up and reflected as overall progress until 100% is reached (a value of e.g. 10 accounts for 10% of work done). Note that currently only `ProgressLocation.Notification` is capable of showing discrete progress.  To monitor if the operation has been cancelled by the user, use the provided `CancellationToken`. Note that currently only `ProgressLocation.Notification` is supporting to show a cancel button to cancel the long running operation. |
    | **Returns**                                                                                                   | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
    | `Thenable<R>`                                                                                                   | The thenable the task-callback returned.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

*   **`withScmProgress<R>(task: (progress: Progress<number>) => Thenable<R>): Thenable<R>`**
    Show progress in the Source Control viewlet while running the given callback and while its returned promise isn't resolve or rejected.

    *   @deprecated - Use `withProgress` instead.

    | Parameter                                                | Description                                                                         |
    | :------------------------------------------------------- | :---------------------------------------------------------------------------------- |
    | `task`: (`progress`: `Progress`<number>) => `Thenable<R>` | A callback returning a promise. Progress increments can be reported with the provided `Progress`-object. |
    | **Returns**                                              | **Description**                                                                     |
    | `Thenable<R>`                                            | The thenable the task did return.                                                   |
