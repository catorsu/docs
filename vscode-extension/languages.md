## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `languages`

Namespace for participating in language-specific editor features, like IntelliSense, code actions, diagnostics etc.

Many programming languages exist and there is huge variety in syntaxes, semantics, and paradigms. Despite that, features like automatic word-completion, code navigation, or code checking have become popular across different tools for different programming languages.

The editor provides an API that makes it simple to provide such common features by having all UI and actions already in place and by allowing you to participate by providing data only. For instance, to contribute a hover all you have to do is provide a function that can be called with a `TextDocument` and a `Position` returning hover info. The rest, like tracking the mouse, positioning the hover, keeping the hover stable etc. is taken care of by the editor.

```javascript
languages.registerHoverProvider('javascript', {
    provideHover(document, position, token) {
        return new Hover('I am a hover!');
    }
});
```

Registration is done using a document selector which is either a language id, like `javascript` or a more complex filter like `{ language: 'typescript', scheme: 'file' }`. Matching a document against such a selector will result in a score that is used to determine if and how a provider shall be used. When scores are equal the provider that came last wins. For features that allow full arity, like hover, the score is only checked to be >0, for other features, like IntelliSense the score is used for determining the order in which providers are asked to participate.

#### Events

*   **`onDidChangeDiagnostics`**: `Event<DiagnosticChangeEvent>`
    An Event which fires when the global set of diagnostics changes. This is newly added and removed diagnostics.

#### Functions

*   **`createDiagnosticCollection(name?: string): DiagnosticCollection`**
    Create a diagnostics collection.

    | Parameter   | Description                |
    | :---------- | :------------------------- |
    | `name?`: string | The name of the collection.  |
    | **Returns** | **Description**            |
    | `DiagnosticCollection` | A new diagnostic collection. |

*   **`createLanguageStatusItem(id: string, selector: DocumentSelector): LanguageStatusItem`**
    Creates a new language status item.

    | Parameter                   | Description                                                              |
    | :-------------------------- | :----------------------------------------------------------------------- |
    | `id`: string                | The identifier of the item.                                              |
    | `selector`: `DocumentSelector` | The document selector that defines for what editors the item shows.      |
    | **Returns**                 | **Description**                                                          |
    | `LanguageStatusItem`        | A new language status item.                                              |

*   **`getDiagnostics(resource: Uri): Diagnostic[]`**
    Get all diagnostics for a given resource.

    | Parameter     | Description                                      |
    | :------------ | :----------------------------------------------- |
    | `resource`: `Uri` | A resource                                       |
    | **Returns**   | **Description**                                  |
    | `Diagnostic[]`  | An array of diagnostics objects or an empty array. |

*   **`getDiagnostics(): Array<[Uri, Diagnostic[]]>`**
    Get all diagnostics.

    | Parameter                       | Description                                                |
    | :------------------------------ | :--------------------------------------------------------- |
    | **Returns**                     | **Description**                                            |
    | `Array<[Uri, Diagnostic[]]>` | An array of uri-diagnostics tuples or an empty array.      |

*   **`getLanguages(): Thenable<string[]>`**
    Return the identifiers of all known languages.

    | Parameter            | Description                                        |
    | :------------------- | :------------------------------------------------- |
    | **Returns**          | **Description**                                    |
    | `Thenable<string[]>` | Promise resolving to an array of identifier strings. |

*   **`match(selector: DocumentSelector, document: TextDocument): number`**
    Compute the match between a document selector and a document. Values greater than zero mean the selector matches the document.

    A match is computed according to these rules:
    1.  When `DocumentSelector` is an array, compute the match for each contained `DocumentFilter` or language identifier and take the maximum value.
    2.  A string will be desugared to become the `language`-part of a `DocumentFilter`, so `"fooLang"` is like `{ language: "fooLang" }`.
    3.  A `DocumentFilter` will be matched against the document by comparing its parts with the document. The following rules apply:
        1.  When the `DocumentFilter` is empty (`{}`) the result is `0`
        2.  When `scheme`, `language`, `pattern`, or `notebook` are defined but one doesn't match, the result is `0`
        3.  Matching against `*` gives a score of `5`, matching via equality or via a glob-pattern gives a score of `10`
        4.  The result is the maximum value of each match

    Samples:
    ```javascript
    // default document from disk (file-scheme)
    doc.uri; //'file:///my/file.js'
    doc.languageId; // 'javascript'
    match('javascript', doc); // 10;
    match({ language: 'javascript' }, doc); // 10;
    match({ language: 'javascript', scheme: 'file' }, doc); // 10;
    match('*', doc); // 5
    match('fooLang', doc); // 0
    match(['fooLang', '*'], doc); // 5

    // virtual document, e.g. from git-index
    doc.uri; // 'git:/my/file.js'
    doc.languageId; // 'javascript'
    match('javascript', doc); // 10;
    match({ language: 'javascript', scheme: 'git' }, doc); // 10;
    match('*', doc); // 5

    // notebook cell document
    doc.uri; // `vscode-notebook-cell:///my/notebook.ipynb#gl65s2pmha`;
    doc.languageId; // 'python'
    match({ notebookType: 'jupyter-notebook' }, doc); // 10
    match({ notebookType: 'fooNotebook', language: 'python' }, doc); // 0
    match({ language: 'python' }, doc); // 10
    match({ notebookType: '*' }, doc); // 5
    ```

    | Parameter                   | Description                                                                 |
    | :-------------------------- | :-------------------------------------------------------------------------- |
    | `selector`: `DocumentSelector` | A document selector.                                                        |
    | `document`: `TextDocument`    | A text document.                                                            |
    | **Returns**                 | **Description**                                                             |
    | `number`                    | A number >0 when the selector matches and 0 when the selector does not match. |

*   **`registerCallHierarchyProvider(selector: DocumentSelector, provider: CallHierarchyProvider): Disposable`**
    Register a call hierarchy provider.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `CallHierarchyProvider` | A call hierarchy provider.                                               |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerCodeActionsProvider(selector: DocumentSelector, provider: CodeActionProvider<CodeAction>, metadata?: CodeActionProviderMetadata): Disposable`**
    Register a code action provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                     | Description                                                              |
    | :-------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `CodeActionProvider<CodeAction>`  | A code action provider.                                                  |
    | `metadata?`: `CodeActionProviderMetadata`     | Metadata about the kind of code actions the provider provides.           |
    | **Returns**                                   | **Description**                                                          |
    | `Disposable`                                  | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerCodeLensProvider(selector: DocumentSelector, provider: CodeLensProvider<CodeLens>): Disposable`**
    Register a code lens provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                   | Description                                                              |
    | :------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`              | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `CodeLensProvider<CodeLens>`    | A code lens provider.                                                    |
    | **Returns**                                 | **Description**                                                          |
    | `Disposable`                                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerColorProvider(selector: DocumentSelector, provider: DocumentColorProvider): Disposable`**
    Register a color provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentColorProvider` | A color provider.                                                        |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerCompletionItemProvider(selector: DocumentSelector, provider: CompletionItemProvider<CompletionItem>, ...triggerCharacters: string[]): Disposable`**
    Register a completion provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and groups of equal score are sequentially asked for completion items. The process stops when one or many providers of a group return a result. A failing provider (rejected promise or exception) will not fail the whole operation.

    A completion item provider can be associated with a set of `triggerCharacters`. When trigger characters are being typed, completions are requested but only from providers that registered the typed character. Because of that trigger characters should be different than word characters, a common trigger character is `.` to trigger member completions.

    | Parameter                                                 | Description                                                              |
    | :-------------------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                            | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `CompletionItemProvider<CompletionItem>`      | A completion provider.                                                   |
    | `...triggerCharacters`: `string[]`                        | Trigger completion when the user types one of the characters.            |
    | **Returns**                                               | **Description**                                                          |
    | `Disposable`                                              | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDeclarationProvider(selector: DocumentSelector, provider: DeclarationProvider): Disposable`**
    Register a declaration provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                       | Description                                                              |
    | :------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`    | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DeclarationProvider` | A declaration provider.                                                  |
    | **Returns**                     | **Description**                                                          |
    | `Disposable`                    | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDefinitionProvider(selector: DocumentSelector, provider: DefinitionProvider): Disposable`**
    Register a definition provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                     | Description                                                              |
    | :---------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`  | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DefinitionProvider` | A definition provider.                                                   |
    | **Returns**                   | **Description**                                                          |
    | `Disposable`                  | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentDropEditProvider(selector: DocumentSelector, provider: DocumentDropEditProvider<DocumentDropEdit>, metadata?: DocumentDropEditProviderMetadata): Disposable`**
    Registers a new `DocumentDropEditProvider`.

    Multiple drop providers can be registered for a language. When dropping content into an editor, all registered providers for the editor's language will be invoked based on the mimetypes they handle as specified by their `DocumentDropEditProviderMetadata`.

    Each provider can return one or more `DocumentDropEdits`. The edits are sorted using the `DocumentDropEdit.yieldTo` property. By default the first edit will be applied. If there are any additional edits, these will be shown to the user as selectable drop options in the drop widget.

    | Parameter                                                       | Description                                                              |
    | :-------------------------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                                  | A selector that defines the documents this provider applies to.          |
    | `provider`: `DocumentDropEditProvider<DocumentDropEdit>`        | A drop provider.                                                         |
    | `metadata?`: `DocumentDropEditProviderMetadata`                 | Additional metadata about the provider.                                  |
    | **Returns**                                                     | **Description**                                                          |
    | `Disposable`                                                    | A `Disposable` that unregisters this provider when disposed of.          |

*   **`registerDocumentFormattingEditProvider(selector: DocumentSelector, provider: DocumentFormattingEditProvider): Disposable`**
    Register a formatting provider for a document.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                                 | Description                                                              |
    | :---------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`            | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentFormattingEditProvider` | A document formatting edit provider.                                     |
    | **Returns**                               | **Description**                                                          |
    | `Disposable`                              | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentHighlightProvider(selector: DocumentSelector, provider: DocumentHighlightProvider): Disposable`**
    Register a document highlight provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and groups sequentially asked for document highlights. The process stops when a provider returns a non-falsy or non-failure result.

    | Parameter                             | Description                                                              |
    | :------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`        | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentHighlightProvider` | A document highlight provider.                                           |
    | **Returns**                           | **Description**                                                          |
    | `Disposable`                          | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentLinkProvider(selector: DocumentSelector, provider: DocumentLinkProvider<DocumentLink>): Disposable`**
    Register a document link provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                         | Description                                                              |
    | :------------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                    | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentLinkProvider<DocumentLink>`  | A document link provider.                                                |
    | **Returns**                                       | **Description**                                                          |
    | `Disposable`                                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentPasteEditProvider(selector: DocumentSelector, provider: DocumentPasteEditProvider<DocumentPasteEdit>, metadata: DocumentPasteProviderMetadata): Disposable`**
    Registers a new `DocumentPasteEditProvider`.

    Multiple providers can be registered for a language. All registered providers for a language will be invoked for copy and paste operations based on their handled mimetypes as specified by the `DocumentPasteProviderMetadata`.

    For copy operations, changes to the `DataTransfer` made by each provider will be merged into a single `DataTransfer` that is used to populate the clipboard.

    For [DocumentPasteEditProvider.providerDocumentPasteEdits paste operations](#DocumentPasteEditProvider.providerDocumentPasteEdits paste operations), each provider will be invoked and can return one or more `DocumentPasteEdits`. The edits are sorted using the `DocumentPasteEdit.yieldTo` property. By default the first edit will be applied and the rest of the edits will be shown to the user as selectable paste options in the paste widget.

    | Parameter                                                         | Description                                                              |
    | :---------------------------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                                    | A selector that defines the documents this provider applies to.          |
    | `provider`: `DocumentPasteEditProvider<DocumentPasteEdit>`        | A paste editor provider.                                                 |
    | `metadata`: `DocumentPasteProviderMetadata`                       | Additional metadata about the provider.                                  |
    | **Returns**                                                       | **Description**                                                          |
    | `Disposable`                                                      | A `Disposable` that unregisters this provider when disposed of.          |

*   **`registerDocumentRangeFormattingEditProvider(selector: DocumentSelector, provider: DocumentRangeFormattingEditProvider): Disposable`**
    Register a formatting provider for a document range.

    Note: A document range provider is also a document formatter which means there is no need to register a document formatter when also registering a range provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                                     | Description                                                              |
    | :-------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentRangeFormattingEditProvider` | A document range formatting edit provider.                               |
    | **Returns**                                   | **Description**                                                          |
    | `Disposable`                                  | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentRangeSemanticTokensProvider(selector: DocumentSelector, provider: DocumentRangeSemanticTokensProvider, legend: SemanticTokensLegend): Disposable`**
    Register a semantic tokens provider for a document range.

    Note: If a document has both a `DocumentSemanticTokensProvider` and a `DocumentRangeSemanticTokensProvider`, the range provider will be invoked only initially, for the time in which the full document provider takes to resolve the first request. Once the full document provider resolves the first request, the semantic tokens provided via the range provider will be discarded and from that point forward, only the document provider will be used.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                                           | Description                                                              |
    | :-------------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentRangeSemanticTokensProvider`   | A document range semantic tokens provider.                               |
    | `legend`: `SemanticTokensLegend`                    |                                                                          |
    | **Returns**                                         | **Description**                                                          |
    | `Disposable`                                        | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentSemanticTokensProvider(selector: DocumentSelector, provider: DocumentSemanticTokensProvider, legend: SemanticTokensLegend): Disposable`**
    Register a semantic tokens provider for a whole document.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                                         | Description                                                              |
    | :------------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                    | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentSemanticTokensProvider`      | A document semantic tokens provider.                                     |
    | `legend`: `SemanticTokensLegend`                  |                                                                          |
    | **Returns**                                       | **Description**                                                          |
    | `Disposable`                                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerDocumentSymbolProvider(selector: DocumentSelector, provider: DocumentSymbolProvider, metaData?: DocumentSymbolProviderMetadata): Disposable`**
    Register a document symbol provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                   | Description                                                              |
    | :------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`              | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `DocumentSymbolProvider`        | A document symbol provider.                                              |
    | `metaData?`: `DocumentSymbolProviderMetadata` | metadata about the provider                                              |
    | **Returns**                                 | **Description**                                                          |
    | `Disposable`                                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerEvaluatableExpressionProvider(selector: DocumentSelector, provider: EvaluatableExpressionProvider): Disposable`**
    Register a provider that locates evaluatable expressions in text documents. The editor will evaluate the expression in the active debug session and will show the result in the debug hover.

    If multiple providers are registered for a language an arbitrary provider will be used.

    | Parameter                                 | Description                                                              |
    | :---------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`            | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `EvaluatableExpressionProvider` | An evaluatable expression provider.                                      |
    | **Returns**                               | **Description**                                                          |
    | `Disposable`                              | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerFoldingRangeProvider(selector: DocumentSelector, provider: FoldingRangeProvider): Disposable`**
    Register a folding range provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. If multiple folding ranges start at the same position, only the range of the first registered provider is used. If a folding range overlaps with an other range that has a smaller position, it is also ignored.

    A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `FoldingRangeProvider`  | A folding range provider.                                                |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerHoverProvider(selector: DocumentSelector, provider: HoverProvider): Disposable`**
    Register a hover provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                   | Description                                                              |
    | :-------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector` | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `HoverProvider`   | A hover provider.                                                        |
    | **Returns**                 | **Description**                                                          |
    | `Disposable`                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerImplementationProvider(selector: DocumentSelector, provider: ImplementationProvider): Disposable`**
    Register an implementation provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                           | Description                                                              |
    | :---------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `ImplementationProvider` | An implementation provider.                                              |
    | **Returns**                         | **Description**                                                          |
    | `Disposable`                        | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerInlayHintsProvider(selector: DocumentSelector, provider: InlayHintsProvider<InlayHint>): Disposable`**
    Register a inlay hints provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                       | Description                                                              |
    | :---------------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`                  | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `InlayHintsProvider<InlayHint>`     | An inlay hints provider.                                                 |
    | **Returns**                                     | **Description**                                                          |
    | `Disposable`                                    | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerInlineCompletionItemProvider(selector: DocumentSelector, provider: InlineCompletionItemProvider): Disposable`**
    Registers an inline completion provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                 | Description                                                              |
    | :---------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`            | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `InlineCompletionItemProvider` | An inline completion provider.                                           |
    | **Returns**                               | **Description**                                                          |
    | `Disposable`                              | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerInlineValuesProvider(selector: DocumentSelector, provider: InlineValuesProvider): Disposable`**
    Register a provider that returns data for the debugger's 'inline value' feature. Whenever the generic debugger has stopped in a source file, providers registered for the language of the file are called to return textual data that will be shown in the editor at the end of lines.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `InlineValuesProvider`  | An inline values provider.                                               |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerLinkedEditingRangeProvider(selector: DocumentSelector, provider: LinkedEditingRangeProvider): Disposable`**
    Register a linked editing range provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider that has a result is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                               | Description                                                              |
    | :-------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`          | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `LinkedEditingRangeProvider` | A linked editing range provider.                                         |
    | **Returns**                             | **Description**                                                          |
    | `Disposable`                            | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerOnTypeFormattingEditProvider(selector: DocumentSelector, provider: OnTypeFormattingEditProvider, firstTriggerCharacter: string, ...moreTriggerCharacter: string[]): Disposable`**
    Register a formatting provider that works on type. The provider is active when the user enables the setting `editor.formatOnType`.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and the best-matching provider is used. Failure of the selected provider will cause a failure of the whole operation.

    | Parameter                                   | Description                                                              |
    | :------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`              | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `OnTypeFormattingEditProvider`  | An on type formatting edit provider.                                     |
    | `firstTriggerCharacter`: string             | A character on which formatting should be triggered, like `}`.           |
    | `...moreTriggerCharacter`: `string[]`       | More trigger characters.                                                 |
    | **Returns**                                 | **Description**                                                          |
    | `Disposable`                                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerReferenceProvider(selector: DocumentSelector, provider: ReferenceProvider): Disposable`**
    Register a reference provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                     | Description                                                              |
    | :---------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`  | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `ReferenceProvider` | A reference provider.                                                    |
    | **Returns**                   | **Description**                                                          |
    | `Disposable`                  | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerRenameProvider(selector: DocumentSelector, provider: RenameProvider): Disposable`**
    Register a rename provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and asked in sequence. The first provider producing a result defines the result of the whole operation.

    | Parameter                   | Description                                                              |
    | :-------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector` | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `RenameProvider`  | A rename provider.                                                       |
    | **Returns**                 | **Description**                                                          |
    | `Disposable`                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerSelectionRangeProvider(selector: DocumentSelector, provider: SelectionRangeProvider): Disposable`**
    Register a selection range provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                             | Description                                                              |
    | :------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`        | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `SelectionRangeProvider`  | A selection range provider.                                              |
    | **Returns**                           | **Description**                                                          |
    | `Disposable`                          | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerSignatureHelpProvider(selector: DocumentSelector, provider: SignatureHelpProvider, ...triggerCharacters: string[]): Disposable`**
    Register a signature help provider.

    Multiple providers can be registered for a language. In that case providers are sorted by their score and called sequentially until a provider returns a valid result.

    | Parameter                               | Description                                                              |
    | :-------------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`          | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `SignatureHelpProvider`     | A signature help provider.                                               |
    | `...triggerCharacters`: `string[]`      | Trigger signature help when the user types one of the characters, like `,` or `(`. |
    | **Returns**                             | **Description**                                                          |
    | `Disposable`                            | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerSignatureHelpProvider(selector: DocumentSelector, provider: SignatureHelpProvider, metadata: SignatureHelpProviderMetadata): Disposable`**
    See also `languages.registerSignatureHelpProvider`

    | Parameter                                   | Description                                                              |
    | :------------------------------------------ | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`              | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `SignatureHelpProvider`         | A signature help provider.                                               |
    | `metadata`: `SignatureHelpProviderMetadata` | Information about the provider.                                          |
    | **Returns**                                 | **Description**                                                          |
    | `Disposable`                                | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerTypeDefinitionProvider(selector: DocumentSelector, provider: TypeDefinitionProvider): Disposable`**
    Register a type definition provider.

    Multiple providers can be registered for a language. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                           | Description                                                              |
    | :---------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `TypeDefinitionProvider` | A type definition provider.                                              |
    | **Returns**                         | **Description**                                                          |
    | `Disposable`                        | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerTypeHierarchyProvider(selector: DocumentSelector, provider: TypeHierarchyProvider): Disposable`**
    Register a type hierarchy provider.

    | Parameter                         | Description                                                              |
    | :-------------------------------- | :----------------------------------------------------------------------- |
    | `selector`: `DocumentSelector`      | A selector that defines the documents this provider is applicable to.    |
    | `provider`: `TypeHierarchyProvider` | A type hierarchy provider.                                               |
    | **Returns**                       | **Description**                                                          |
    | `Disposable`                      | A `Disposable` that unregisters this provider when being disposed.       |

*   **`registerWorkspaceSymbolProvider(provider: WorkspaceSymbolProvider<SymbolInformation>): Disposable`**
    Register a workspace symbol provider.

    Multiple providers can be registered. In that case providers are asked in parallel and the results are merged. A failing provider (rejected promise or exception) will not cause a failure of the whole operation.

    | Parameter                                               | Description                                                              |
    | :------------------------------------------------------ | :----------------------------------------------------------------------- |
    | `provider`: `WorkspaceSymbolProvider<SymbolInformation>` | A workspace symbol provider.                                             |
    | **Returns**                                             | **Description**                                                          |
    | `Disposable`                                            | A `Disposable` that unregisters this provider when being disposed.       |

*   **`setLanguageConfiguration(language: string, configuration: LanguageConfiguration): Disposable`**
    Set a language configuration for a language.

    | Parameter                               | Description                                                        |
    | :-------------------------------------- | :----------------------------------------------------------------- |
    | `language`: string                      | A language identifier like `typescript`.                           |
    | `configuration`: `LanguageConfiguration` | Language configuration.                                            |
    | **Returns**                             | **Description**                                                    |
    | `Disposable`                            | A `Disposable` that unsets this configuration.                     |

*   **`setTextDocumentLanguage(document: TextDocument, languageId: string): Thenable<TextDocument>`**
    Set (and change) the language that is associated with the given document.

    Note that calling this function will trigger the `onDidCloseTextDocument` event followed by the `onDidOpenTextDocument` event.

    | Parameter                 | Description                                      |
    | :------------------------ | :----------------------------------------------- |
    | `document`: `TextDocument`  | The document which language is to be changed     |
    | `languageId`: string      | The new language identifier.                     |
    | **Returns**               | **Description**                                  |
    | `Thenable<TextDocument>`  | A thenable that resolves with the updated document. |

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