## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `tests`

Namespace for testing functionality. Tests are published by registering `TestController` instances, then adding `TestItems`. Controllers may also describe how to run tests by creating one or more `TestRunProfile` instances.

#### Functions

*   **`createTestController(id: string, label: string): TestController`**
    Creates a new test controller.

    | Parameter           | Description                                                |
    | :------------------ | :--------------------------------------------------------- |
    | `id`: string        | Identifier for the controller, must be globally unique.    |
    | `label`: string     | A human-readable label for the controller.                 |
    | **Returns**         | **Description**                                            |
    | `TestController`    | An instance of the `TestController`.                       |