## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `tasks`

Namespace for tasks functionality.

#### Variables

*   **`taskExecutions`**: `readonly TaskExecution[]`
    The currently active task executions or an empty array.

#### Events

*   **`onDidEndTask`**: `Event<TaskEndEvent>`
    Fires when a task ends.
*   **`onDidEndTaskProcess`**: `Event<TaskProcessEndEvent>`
    Fires when the underlying process has ended. This event will not fire for tasks that don't execute an underlying process.
*   **`onDidStartTask`**: `Event<TaskStartEvent>`
    Fires when a task starts.
*   **`onDidStartTaskProcess`**: `Event<TaskProcessStartEvent>`
    Fires when the underlying process has been started. This event will not fire for tasks that don't execute an underlying process.

#### Functions

*   **`executeTask(task: Task): Thenable<TaskExecution>`**
    Executes a task that is managed by the editor. The returned task execution can be used to terminate the task.
    *   throws - When running a `ShellExecution` or a `ProcessExecution` task in an environment where a new process cannot be started. In such an environment, only `CustomExecution` tasks can be run.

    | Parameter               | Description                                  |
    | :---------------------- | :------------------------------------------- |
    | `task`: `Task`          | the task to execute                          |
    | **Returns**             | **Description**                              |
    | `Thenable<TaskExecution>` | A thenable that resolves to a task execution. |

*   **`fetchTasks(filter?: TaskFilter): Thenable<Task[]>`**
    Fetches all tasks available in the systems. This includes tasks from `tasks.json` files as well as tasks from task providers contributed through extensions.

    | Parameter             | Description                                                              |
    | :-------------------- | :----------------------------------------------------------------------- |
    | `filter?`: `TaskFilter` | Optional filter to select tasks of a certain type or version.            |
    | **Returns**           | **Description**                                                          |
    | `Thenable<Task[]>`    | A thenable that resolves to an array of tasks.                           |

*   **`registerTaskProvider(type: string, provider: TaskProvider<Task>): Disposable`**
    Register a task provider.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `type`: string                    | The task kind type this provider is registered for.                      |
    | `provider`: `TaskProvider<Task>`  | A task provider.                                                         |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |