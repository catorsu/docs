## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `scm`

Namespace for source control management.

#### Variables

*   **`inputBox`**: `SourceControlInputBox`
    The input box for the last source control created by the extension.
    *   deprecated - Use `SourceControl.inputBox` instead

#### Functions

*   **`createSourceControl(id: string, label: string, rootUri?: Uri): SourceControl`**
    Creates a new source control instance.

    | Parameter         | Description                                                              |
    | :---------------- | :----------------------------------------------------------------------- |
    | `id`: string      | An id for the source control. Something short, e.g.: `git`.              |
    | `label`: string   | A human-readable string for the source control. E.g.: `Git`.             |
    | `rootUri?`: `Uri` | An optional `Uri` of the root of the source control. E.g.: `Uri.parse(workspaceRoot)`. |
    | **Returns**       | **Description**                                                          |
    | `SourceControl`   | An instance of source control.                                           |