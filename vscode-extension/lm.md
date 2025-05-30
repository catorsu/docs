## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `lm`

Namespace for language model related functionality.

#### Variables

*   **`tools`**: `readonly LanguageModelToolInformation[]`
    A list of all available tools that were registered by all extensions using `lm.registerTool`. They can be called with `lm.invokeTool` with input that match their declared `inputSchema`.

#### Events

*   **`onDidChangeChatModels`**: `Event<void>`
    An event that is fired when the set of available chat models changes.

#### Functions

*   **`invokeTool(name: string, options: LanguageModelToolInvocationOptions<object>, token?: CancellationToken): Thenable<LanguageModelToolResult>`**
    Invoke a tool listed in `lm.tools` by name with the given input. The input will be validated against the schema declared by the tool.

    A tool can be invoked by a chat participant, in the context of handling a chat request, or globally by any extension in any custom flow.

    In the former case, the caller shall pass the `toolInvocationToken`, which comes with the a chat request. This makes sure the chat UI shows the tool invocation for the correct conversation.

    A tool result is an array of text- and `prompt-tsx`-parts. If the tool caller is using `vscode/prompt-tsx`, it can incorporate the response parts into its prompt using a `ToolResult`. If not, the parts can be passed along to the `LanguageModelChat` via a user message with a `LanguageModelToolResultPart`.

    If a chat participant wants to preserve tool results for requests across multiple turns, it can store tool results in the `ChatResult.metadata` returned from the handler and retrieve them on the next turn from `ChatResponseTurn.result`.

    | Parameter                                                              | Description                                                              |
    | :--------------------------------------------------------------------- | :----------------------------------------------------------------------- |
    | `name`: string                                                         | The name of the tool to call.                                            |
    | `options`: `LanguageModelToolInvocationOptions<object>`                | The options to use when invoking the tool.                               |
    | `token?`: `CancellationToken`                                          | A cancellation token. See `CancellationTokenSource` for how to create one. |
    | **Returns**                                                            | **Description**                                                          |
    | `Thenable<LanguageModelToolResult>`                                    | The result of the tool invocation.                                       |

*   **`registerTool<T>(name: string, tool: LanguageModelTool<T>): Disposable`**
    Register a `LanguageModelTool`. The tool must also be registered in the `package.json` `languageModelTools` contribution point. A registered tool is available in the `lm.tools` list for any extension to see. But in order for it to be seen by a language model, it must be passed in the list of available tools in `LanguageModelChatRequestOptions.tools`.

    | Parameter                        | Description                                                  |
    | :------------------------------- | :----------------------------------------------------------- |
    | `name`: string                   |                                                              |
    | `tool`: `LanguageModelTool<T>`   |                                                              |
    | **Returns**                      | **Description**                                              |
    | `Disposable`                     | A `Disposable` that unregisters the tool when disposed.      |

*   **`selectChatModels(selector?: LanguageModelChatSelector): Thenable<LanguageModelChat[]>`**
    Select chat models by a selector. This can yield multiple or no chat models and extensions must handle these cases, esp. when no chat model exists, gracefully.

    ```javascript
    const models = await vscode.lm.selectChatModels({ family: 'gpt-3.5-turbo' });
    if (models.length > 0) {
        const [first] = models;
        const response = await first.sendRequest(...)
        // ...
    } else {
        // NO chat models available
    }
    ```

    A selector can be written to broadly match all models of a given vendor or family, or it can narrowly select one model by ID. Keep in mind that the available set of models will change over time, but also that prompts may perform differently in different models.

    Note that extensions can hold on to the results returned by this function and use them later. However, when the `onDidChangeChatModels`-event is fired the list of chat models might have changed and extensions should re-query.

    | Parameter                               | Description                                                              |
    | :-------------------------------------- | :----------------------------------------------------------------------- |
    | `selector?`: `LanguageModelChatSelector` | A chat model selector. When omitted all chat models are returned.        |
    | **Returns**                             | **Description**                                                          |
    | `Thenable<LanguageModelChat[]>`         | An array of chat models, can be empty!                                   |