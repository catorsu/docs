## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `chat`

Namespace for chat functionality. Users interact with chat participants by sending messages to them in the chat view. Chat participants can respond with markdown or other types of content via the `ChatResponseStream`.

#### Functions

*   **`createChatParticipant(id: string, handler: ChatRequestHandler): ChatParticipant`**
    Create a new chat participant instance.

    | Parameter                    | Description                        |
    | :--------------------------- | :--------------------------------- |
    | `id`: string                 | A unique identifier for the participant. |
    | `handler`: `ChatRequestHandler` | A request handler for the participant. |
    | **Returns**                  | **Description**                    |
    | `ChatParticipant`            | A new chat participant             |