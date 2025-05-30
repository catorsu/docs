## API namespaces and classes

This listing is compiled from the `vscode.d.ts` file from the VS Code repository.

## `authentication`

Namespace for authentication.

#### Events

*   **`onDidChangeSessions`**: `Event<AuthenticationSessionsChangeEvent>`
    An Event which fires when the authentication sessions of an authentication provider have been added, removed, or changed.

#### Functions

*   **`getAccounts(providerId: string): Thenable<readonly AuthenticationSessionAccountInformation[]>`**
    Get all accounts that the user is logged in to for the specified provider. Use this paired with `getSession` in order to get an authentication session for a specific account.

    Currently, there are only two authentication providers that are contributed from built in extensions to the editor that implement GitHub and Microsoft authentication: their `providerId`'s are 'github' and 'microsoft'.

    Note: Getting accounts does not imply that your extension has access to that account or its authentication sessions. You can verify access to the account by calling `getSession`.

    | Parameter        | Description                                  |
    | :--------------- | :------------------------------------------- |
    | `providerId`: string | The id of the provider to use                |
    | **Returns**      | **Description**                              |
    | `Thenable<readonly AuthenticationSessionAccountInformation[]>` | A thenable that resolves to a readonly array of authentication accounts. |

*   **`getSession(providerId: string, scopes: readonly string[], options: AuthenticationGetSessionOptions & {createIfNone: true | AuthenticationGetSessionPresentationOptions}): Thenable<AuthenticationSession>`**
    Get an authentication session matching the desired scopes. Rejects if a provider with `providerId` is not registered, or if the user does not consent to sharing authentication information with the extension. If there are multiple sessions with the same scopes, the user will be shown a quickpick to select which account they would like to use.

    Currently, there are only two authentication providers that are contributed from built in extensions to the editor that implement GitHub and Microsoft authentication: their `providerId`'s are 'github' and 'microsoft'.

    | Parameter                                                                                             | Description                                                                                                |
    | :---------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
    | `providerId`: string                                                                                    | The id of the provider to use                                                                              |
    | `scopes`: readonly string[]                                                                             | A list of scopes representing the permissions requested. These are dependent on the authentication provider |
    | `options`: `AuthenticationGetSessionOptions` & {`createIfNone`: `true` \| `AuthenticationGetSessionPresentationOptions`} | The `AuthenticationGetSessionOptions` to use                                                               |
    | **Returns**                                                                                           | **Description**                                                                                            |
    | `Thenable<AuthenticationSession>`                                                                       | A thenable that resolves to an authentication session                                                      |

*   **`getSession(providerId: string, scopes: readonly string[], options: AuthenticationGetSessionOptions & {forceNewSession: true | AuthenticationGetSessionPresentationOptions}): Thenable<AuthenticationSession>`**
    Get an authentication session matching the desired scopes. Rejects if a provider with `providerId` is not registered, or if the user does not consent to sharing authentication information with the extension. If there are multiple sessions with the same scopes, the user will be shown a quickpick to select which account they would like to use.

    Currently, there are only two authentication providers that are contributed from built in extensions to the editor that implement GitHub and Microsoft authentication: their `providerId`'s are 'github' and 'microsoft'.

    | Parameter                                                                                               | Description                                                                                                |
    | :------------------------------------------------------------------------------------------------------ | :--------------------------------------------------------------------------------------------------------- |
    | `providerId`: string                                                                                      | The id of the provider to use                                                                              |
    | `scopes`: readonly string[]                                                                               | A list of scopes representing the permissions requested. These are dependent on the authentication provider |
    | `options`: `AuthenticationGetSessionOptions` & {`forceNewSession`: `true` \| `AuthenticationGetSessionPresentationOptions`} | The `AuthenticationGetSessionOptions` to use                                                               |
    | **Returns**                                                                                             | **Description**                                                                                            |
    | `Thenable<AuthenticationSession>`                                                                         | A thenable that resolves to an authentication session                                                      |

*   **`getSession(providerId: string, scopes: readonly string[], options?: AuthenticationGetSessionOptions): Thenable<AuthenticationSession | undefined>`**
    Get an authentication session matching the desired scopes. Rejects if a provider with `providerId` is not registered, or if the user does not consent to sharing authentication information with the extension. If there are multiple sessions with the same scopes, the user will be shown a quickpick to select which account they would like to use.

    Currently, there are only two authentication providers that are contributed from built in extensions to the editor that implement GitHub and Microsoft authentication: their `providerId`'s are 'github' and 'microsoft'.

    | Parameter                               | Description                                                                                                |
    | :-------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
    | `providerId`: string                    | The id of the provider to use                                                                              |
    | `scopes`: readonly string[]             | A list of scopes representing the permissions requested. These are dependent on the authentication provider |
    | `options?`: `AuthenticationGetSessionOptions` | The `AuthenticationGetSessionOptions` to use                                                               |
    | **Returns**                             | **Description**                                                                                            |
    | `Thenable<AuthenticationSession | undefined>` | A thenable that resolves to an authentication session if available, or `undefined` if there are no sessions |

*   **`registerAuthenticationProvider(id: string, label: string, provider: AuthenticationProvider, options?: AuthenticationProviderOptions): Disposable`**
    Register an authentication provider.

    There can only be one provider per id and an error is being thrown when an id has already been used by another provider. Ids are case-sensitive.

    | Parameter                               | Description                                                        |
    | :-------------------------------------- | :----------------------------------------------------------------- |
    | `id`: string                            | The unique identifier of the provider.                             |
    | `label`: string                         | The human-readable name of the provider.                           |
    | `provider`: `AuthenticationProvider`      | The authentication provider provider.                              |
    | `options?`: `AuthenticationProviderOptions` | Additional options for the provider.                               |
    | **Returns**                             | **Description**                                                    |
    | `Disposable`                            | A `Disposable` that unregisters this provider when being disposed. |