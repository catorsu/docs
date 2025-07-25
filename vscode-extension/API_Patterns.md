## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## API Patterns

These are some of the common patterns we use in the VS Code API.

### Promises

The VS Code API represents asynchronous operations with promises. From extensions, any type of promise can be returned, like ES6, WinJS, A+, etc.

Being independent of a specific promise library is expressed in the API by the `Thenable`-type. `Thenable` represents the common denominator which is the `then` method.

In most cases the use of promises is optional and when VS Code calls into an extension, it can handle the result type as well as a `Thenable` of the result type. When the use of a promise is optional, the API indicates this by returning or-types.

```typescript
provideNumber(): number | Thenable<number>
```

### Cancellation Tokens

Often operations are started on volatile state which changes before operations can finish. For instance, computing IntelliSense starts and the user continues to type making the result of that operation obsolete.

APIs that are exposed to such behavior will get passed a `CancellationToken` on which you can check for cancellation (`isCancellationRequested`) or get notified when cancellation occurs (`onCancellationRequested`). The cancellation token is usually the last parameter of a function call and optional.

### Disposables

The VS Code API uses the dispose pattern for resources that are obtained from VS Code. This applies to event listening, commands, interacting with the UI, and various language contributions.

For instance, the `setStatusBarMessage(value: string)` function returns a `Disposable` which upon calling `dispose` removes the message again.

### Events

Events in the VS Code API are exposed as functions which you call with a listener-function to subscribe. Calls to subscribe return a `Disposable` which removes the event listener upon `dispose`.

```javascript
var listener = function(event) {
    console.log('It happened', event);
};

// start listening
var subscription = fsWatcher.onDidDelete(listener);

// do more stuff
subscription.dispose(); // stop listening
```

Names of events follow the `on[Will|Did]VerbNoun?` pattern. The name signals if the event is going to happen (`onWill`) or already happened (`onDid`), what happened (verb), and the context (noun) unless obvious from the context.

An example from the VS Code API is `window.onDidChangeActiveTextEditor` which is an event fired when the active text editor (noun) has been (`onDid`) changed (verb).

### Strict null

The VS Code API uses the `undefined` and `null` TypeScript types where appropriate to support strict null checking.
