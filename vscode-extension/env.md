## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `env`

Namespace describing the environment the editor runs in.

#### Variables

*   **`appHost`**: `string`
    The hosted location of the application. On desktop this is 'desktop'. In the web this is the specified embedder i.e. 'github.dev', 'codespaces', or 'web' if the embedder does not provide that information.
*   **`appName`**: `string`
    The application name of the editor, like 'VS Code'.
*   **`appRoot`**: `string`
    The application root folder from which the editor is running.
    Note that the value is the empty string when running in an environment that has no representation of an application root folder.
*   **`clipboard`**: `Clipboard`
    The system clipboard.
*   **`isNewAppInstall`**: `boolean`
    Indicates that this is a fresh install of the application. `true` if within the first day of installation otherwise `false`.
*   **`isTelemetryEnabled`**: `boolean`
    Indicates whether the users has telemetry enabled. Can be observed to determine if the extension should send telemetry.
*   **`language`**: `string`
    Represents the preferred user-language, like `de-CH`, `fr`, or `en-US`.
*   **`logLevel`**: `LogLevel`
    The current log level of the editor.
*   **`machineId`**: `string`
    A unique identifier for the computer.
*   **`remoteName`**: `string | undefined`
    The name of a remote. Defined by extensions, popular samples are `wsl` for the Windows Subsystem for Linux or `ssh-remote` for remotes using a secure shell.
    Note that the value is `undefined` when there is no remote extension host but that the value is defined in all extension hosts (local and remote) in case a remote extension host exists. Use `Extension.extensionKind` to know if a specific extension runs remote or not.
*   **`sessionId`**: `string`
    A unique identifier for the current session. Changes each time the editor is started.
*   **`shell`**: `string`
    The detected default shell for the extension host, this is overridden by the `terminal.integrated.defaultProfile` setting for the extension host's platform. Note that in environments that do not support a shell the value is the empty string.
*   **`uiKind`**: `UIKind`
    The UI kind property indicates from which UI extensions are accessed from. For example, extensions could be accessed from a desktop application or a web browser.
*   **`uriScheme`**: `string`
    The custom uri scheme the editor registers to in the operating system.

#### Events

*   **`onDidChangeLogLevel`**: `Event<LogLevel>`
    An Event which fires when the log level of the editor changes.
*   **`onDidChangeShell`**: `Event<string>`
    An Event which fires when the default shell changes. This fires with the new shell path.
*   **`onDidChangeTelemetryEnabled`**: `Event<boolean>`
    An Event which fires when the user enabled or disables telemetry. `true` if the user has enabled telemetry or `false` if the user has disabled telemetry.

#### Functions

*   **`asExternalUri(target: Uri): Thenable<Uri>`**
    Resolves a `Uri` to a form that is accessible externally.

    #### `http:` or `https:` scheme
    Resolves an external `Uri`, such as a `http:` or `https:` link, from where the extension is running to a `Uri` to the same resource on the client machine.

    This is a no-op if the extension is running on the client machine.

    If the extension is running remotely, this function automatically establishes a port forwarding tunnel from the local machine to `target` on the remote and returns a local `Uri` to the tunnel. The lifetime of the port forwarding tunnel is managed by the editor and the tunnel can be closed by the user.

    Note that uris passed through `openExternal` are automatically resolved and you should not call `asExternalUri` on them.

    #### `vscode.env.uriScheme`
    Creates a `Uri` that - if opened in a browser (e.g. via `openExternal`) - will result in a registered `UriHandler` to trigger.

    Extensions should not make any assumptions about the resulting `Uri` and should not alter it in any way. Rather, extensions can e.g. use this `Uri` in an authentication flow, by adding the `Uri` as callback query argument to the server to authenticate to.

    Note that if the server decides to add additional query parameters to the `Uri` (e.g. a token or secret), it will appear in the `Uri` that is passed to the `UriHandler`.

    Example of an authentication flow:
    ```javascript
    vscode.window.registerUriHandler({ handleUri(uri: vscode.Uri): vscode.ProviderResult<void> { if (uri.path === '/did-authenticate') { console.log(uri.toString()); } } });
    const callableUri = await vscode.env.asExternalUri( vscode.Uri.parse(vscode.env.uriScheme + '://my.extension/did-authenticate') );
    await vscode.env.openExternal(callableUri);
    ```

    Note that extensions should not cache the result of `asExternalUri` as the resolved `Uri` may become invalid due to a system or user action — for example, in remote cases, a user may close a port forwarding tunnel that was opened by `asExternalUri`.

    #### Any other scheme
    Any other scheme will be handled as if the provided `URI` is a workspace `URI`. In that case, the method will return a `URI` which, when handled, will make the editor open the workspace.

    | Parameter   | Description                                      |
    | :---------- | :----------------------------------------------- |
    | `target`: `Uri` |                                                  |
    | **Returns** | **Description**                                  |
    | `Thenable<Uri>` | A `Uri` that can be used on the client machine. |

*   **`createTelemetryLogger(sender: TelemetrySender, options?: TelemetryLoggerOptions): TelemetryLogger`**
    Creates a new telemetry logger.

    | Parameter                         | Description                                               |
    | :-------------------------------- | :-------------------------------------------------------- |
    | `sender`: `TelemetrySender`         | The telemetry sender that is used by the telemetry logger. |
    | `options?`: `TelemetryLoggerOptions` | Options for the telemetry logger.                         |
    | **Returns**                       | **Description**                                           |
    | `TelemetryLogger`                 | A new telemetry logger                                    |

*   **`openExternal(target: Uri): Thenable<boolean>`**
    Opens a link externally using the default application. Depending on the used scheme this can be:
    *   a browser (`http:`, `https:`)
    *   a mail client (`mailto:`)
    *   VSCode itself (`vscode:` from `vscode.env.uriScheme`)

    Note that `showTextDocument` is the right way to open a text document inside the editor, not this function.

    | Parameter       | Description                               |
    | :-------------- | :---------------------------------------- |
    | `target`: `Uri`   | The `Uri` that should be opened.          |
    | **Returns**     | **Description**                           |
    | `Thenable<boolean>` | A promise indicating if open was successful. |