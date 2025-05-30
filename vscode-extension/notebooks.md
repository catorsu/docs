## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `notebooks`

Namespace for notebooks.

The notebooks functionality is composed of three loosely coupled components:
1.  `NotebookSerializer` enable the editor to open, show, and save notebooks
2.  `NotebookController` own the execution of notebooks, e.g they create output from code cells.
3.  `NotebookRenderer` present notebook output in the editor. They run in a separate context.

#### Functions

*   **`createNotebookController(id: string, notebookType: string, label: string, handler?: (cells: NotebookCell[], notebook: NotebookDocument, controller: NotebookController) => void | Thenable<void>): NotebookController`**
    Creates a new notebook controller.

    | Parameter                                                                                                             | Description                                                        |
    | :-------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------- |
    | `id`: string                                                                                                          | Identifier of the controller. Must be unique per extension.        |
    | `notebookType`: string                                                                                                | A notebook type for which this controller is for.                  |
    | `label`: string                                                                                                       | The label of the controller.                                       |
    | `handler?`: `(cells: NotebookCell[], notebook: NotebookDocument, controller: NotebookController) => void | Thenable<void>` | The execute-handler of the controller.                             |
    | **Returns**                                                                                                           | **Description**                                                    |
    | `NotebookController`                                                                                                  | A new notebook controller.                                         |

*   **`createRendererMessaging(rendererId: string): NotebookRendererMessaging`**
    Creates a new messaging instance used to communicate with a specific renderer.

    *   Note 1: Extensions can only create renderer that they have defined in their `package.json`-file
    *   Note 2: A renderer only has access to messaging if `requiresMessaging` is set to `always` or `optional` in its `notebookRenderer` contribution.

    | Parameter                   | Description                                  |
    | :-------------------------- | :------------------------------------------- |
    | `rendererId`: string        | The renderer ID to communicate with          |
    | **Returns**                 | **Description**                              |
    | `NotebookRendererMessaging` | A new notebook renderer messaging object.    |

*   **`registerNotebookCellStatusBarItemProvider(notebookType: string, provider: NotebookCellStatusBarItemProvider): Disposable`**
    Register a cell statusbar item provider for the given notebook type.

    | Parameter                                         | Description                                                              |
    | :------------------------------------------------ | :----------------------------------------------------------------------- |
    | `notebookType`: string                            | The notebook type to register for.                                       |
    | `provider`: `NotebookCellStatusBarItemProvider`   | A cell status bar provider.                                              |
    | **Returns**                                       | **Description**                                                          |
    | `Disposable`                                      | A `Disposable` that unregisters this provider when being disposed.       |