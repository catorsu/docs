## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `debug`

Namespace for debug functionality.

#### Variables

*   **`activeDebugConsole`**: `DebugConsole`
    The currently active debug console. If no debug session is active, output sent to the debug console is not shown.
*   **`activeDebugSession`**: `DebugSession | undefined`
    The currently active debug session or `undefined`. The active debug session is the one represented by the debug action floating window or the one currently shown in the drop down menu of the debug action floating window. If no debug session is active, the value is `undefined`.
*   **`activeStackItem`**: `DebugThread | DebugStackFrame | undefined`
    The currently focused thread or stack frame, or `undefined` if no thread or stack is focused. A thread can be focused any time there is an active debug session, while a stack frame can only be focused when a session is paused and the call stack has been retrieved.
*   **`breakpoints`**: `readonly Breakpoint[]`
    List of breakpoints.

#### Events

*   **`onDidChangeActiveDebugSession`**: `Event<DebugSession | undefined>`
    An Event which fires when the active debug session has changed. Note that the event also fires when the active debug session changes to `undefined`.
*   **`onDidChangeActiveStackItem`**: `Event<DebugThread | DebugStackFrame | undefined>`
    An event which fires when the `debug.activeStackItem` has changed.
*   **`onDidChangeBreakpoints`**: `Event<BreakpointsChangeEvent>`
    An Event that is emitted when the set of breakpoints is added, removed, or changed.
*   **`onDidReceiveDebugSessionCustomEvent`**: `Event<DebugSessionCustomEvent>`
    An Event which fires when a custom DAP event is received from the debug session.
*   **`onDidStartDebugSession`**: `Event<DebugSession>`
    An Event which fires when a new debug session has been started.
*   **`onDidTerminateDebugSession`**: `Event<DebugSession>`
    An Event which fires when a debug session has terminated.

#### Functions

*   **`addBreakpoints(breakpoints: readonly Breakpoint[]): void`**
    Add breakpoints.

    | Parameter                          | Description              |
    | :--------------------------------- | :----------------------- |
    | `breakpoints`: readonly `Breakpoint[]` | The breakpoints to add.  |
    | **Returns**                        | **Description**          |
    | `void`                             |                          |

*   **`asDebugSourceUri(source: DebugProtocolSource, session?: DebugSession): Uri`**
    Converts a "Source" descriptor object received via the Debug Adapter Protocol into a `Uri` that can be used to load its contents. If the source descriptor is based on a path, a file `Uri` is returned. If the source descriptor uses a reference number, a specific debug `Uri` (scheme 'debug') is constructed that requires a corresponding `ContentProvider` and a running debug session.

    If the "Source" descriptor has insufficient information for creating the `Uri`, an error is thrown.

    | Parameter                   | Description                                                                                                                                        |
    | :-------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `source`: `DebugProtocolSource` | An object conforming to the Source type defined in the Debug Adapter Protocol.                                                                     |
    | `session?`: `DebugSession`    | An optional debug session that will be used when the source descriptor uses a reference number to load the contents from an active debug session. |
    | **Returns**                 | **Description**                                                                                                                                    |
    | `Uri`                       | A `Uri` that can be used to load the contents of the source.                                                                                       |

*   **`registerDebugAdapterDescriptorFactory(debugType: string, factory: DebugAdapterDescriptorFactory): Disposable`**
    Register a debug adapter descriptor factory for a specific debug type. An extension is only allowed to register a `DebugAdapterDescriptorFactory` for the debug type(s) defined by the extension. Otherwise an error is thrown. Registering more than one `DebugAdapterDescriptorFactory` for a debug type results in an error.

    | Parameter                               | Description                                                              |
    | :-------------------------------------- | :----------------------------------------------------------------------- |
    | `debugType`: string                     | The debug type for which the factory is registered.                      |
    | `factory`: `DebugAdapterDescriptorFactory` | The debug adapter descriptor factory to register.                        |
    | **Returns**                             | **Description**                                                          |
    | `Disposable`                            | A `Disposable` that unregisters this factory when being disposed.        |

*   **`registerDebugAdapterTrackerFactory(debugType: string, factory: DebugAdapterTrackerFactory): Disposable`**
    Register a debug adapter tracker factory for the given debug type.

    | Parameter                           | Description                                                                      |
    | :---------------------------------- | :------------------------------------------------------------------------------- |
    | `debugType`: string                 | The debug type for which the factory is registered or `*` for matching all debug types. |
    | `factory`: `DebugAdapterTrackerFactory` | The debug adapter tracker factory to register.                                   |
    | **Returns**                         | **Description**                                                                  |
    | `Disposable`                        | A `Disposable` that unregisters this factory when being disposed.                |

*   **`registerDebugConfigurationProvider(debugType: string, provider: DebugConfigurationProvider, triggerKind?: DebugConfigurationProviderTriggerKind): Disposable`**
    Register a debug configuration provider for a specific debug type. The optional `triggerKind` can be used to specify when the `provideDebugConfigurations` method of the provider is triggered. Currently two trigger kinds are possible: with the value `Initial` (or if no trigger kind argument is given) the `provideDebugConfigurations` method is used to provide the initial debug configurations to be copied into a newly created `launch.json`. With the trigger kind `Dynamic` the `provideDebugConfigurations` method is used to dynamically determine debug configurations to be presented to the user (in addition to the static configurations from the `launch.json`). Please note that the `triggerKind` argument only applies to the `provideDebugConfigurations` method: so the `resolveDebugConfiguration` methods are not affected at all. Registering a single provider with resolve methods for different trigger kinds, results in the same resolve methods called multiple times. More than one provider can be registered for the same type.

    | Parameter                                                 | Description                                                                                                                                                           |
    | :-------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
    | `debugType`: string                                       | The debug type for which the provider is registered.                                                                                                                  |
    | `provider`: `DebugConfigurationProvider`                  | The debug configuration provider to register.                                                                                                                         |
    | `triggerKind?`: `DebugConfigurationProviderTriggerKind` | The trigger for which the 'provideDebugConfiguration' method of the provider is registered. If `triggerKind` is missing, the value `DebugConfigurationProviderTriggerKind.Initial` is assumed. |
    | **Returns**                                               | **Description**                                                                                                                                                       |
    | `Disposable`                                              | A `Disposable` that unregisters this provider when being disposed.                                                                                                    |

*   **`removeBreakpoints(breakpoints: readonly Breakpoint[]): void`**
    Remove breakpoints.

    | Parameter                          | Description                |
    | :--------------------------------- | :------------------------- |
    | `breakpoints`: readonly `Breakpoint[]` | The breakpoints to remove. |
    | **Returns**                        | **Description**            |
    | `void`                             |                            |

*   **`startDebugging(folder: WorkspaceFolder, nameOrConfiguration: string | DebugConfiguration, parentSessionOrOptions?: DebugSession | DebugSessionOptions): Thenable<boolean>`**
    Start debugging by using either a named launch or named compound configuration, or by directly passing a `DebugConfiguration`. The named configurations are looked up in `.vscode/launch.json` found in the given folder. Before debugging starts, all unsaved files are saved and the launch configurations are brought up-to-date. Folder specific variables used in the configuration (e.g. `${workspaceFolder}`) are resolved against the given folder.

    | Parameter                                                                 | Description                                                                                                                            |
    | :------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------- |
    | `folder`: `WorkspaceFolder`                                               | The workspace folder for looking up named configurations and resolving variables or `undefined` for a non-folder setup.                |
    | `nameOrConfiguration`: string \| `DebugConfiguration`                     | Either the name of a debug or compound configuration or a `DebugConfiguration` object.                                                 |
    | `parentSessionOrOptions?`: `DebugSession` \| `DebugSessionOptions`        | Debug session options. When passed a parent debug session, assumes options with just this parent session.                              |
    | **Returns**                                                               | **Description**                                                                                                                        |
    | `Thenable<boolean>`                                                       | A thenable that resolves when debugging could be successfully started.                                                                 |

*   **`stopDebugging(session?: DebugSession): Thenable<void>`**
    Stop the given debug session or stop all debug sessions if `session` is omitted.

    | Parameter             | Description                                                              |
    | :-------------------- | :----------------------------------------------------------------------- |
    | `session?`: `DebugSession` | The debug session to stop; if omitted all sessions are stopped.          |
    | **Returns**           | **Description**                                                          |
    | `Thenable<void>`      | A thenable that resolves when the session(s) have been stopped.          |