## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `extensions`

Namespace for dealing with installed extensions. Extensions are represented by an `Extension`-interface which enables reflection on them.

Extension writers can provide APIs to other extensions by returning their API public surface from the `activate`-call.

```javascript
export function activate(context: vscode.ExtensionContext) {
    let api = {
        sum(a, b) { return a + b; },
        mul(a, b) { return a * b; }
    };
    // 'export' public api-surface
    return api;
}
```

When depending on the API of another extension add an `extensionDependencies`-entry to `package.json`, and use the `getExtension`-function and the `exports`-property, like below:

```javascript
let mathExt = extensions.getExtension('genius.math');
let importedApi = mathExt.exports;
console.log(importedApi.mul(42, 1));
```

#### Variables

*   **`all`**: `readonly Extension<any>[]`
    All extensions currently known to the system.

#### Events

*   **`onDidChange`**: `Event<void>`
    An event which fires when `extensions.all` changes. This can happen when extensions are installed, uninstalled, enabled or disabled.

#### Functions

*   **`getExtension<T>(extensionId: string): Extension<T> | undefined`**
    Get an extension by its full identifier in the form of: `publisher.name`.

    | Parameter           | Description              |
    | :------------------ | :----------------------- |
    | `extensionId`: string | An extension identifier. |
    | **Returns**         | **Description**          |
    | `Extension<T> | undefined` | An extension or `undefined`. |
