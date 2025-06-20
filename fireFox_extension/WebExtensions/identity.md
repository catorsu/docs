# identity

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/identity
- **Version**: WebExtensions API

## Overview

Use the identity API to get an OAuth2 authorization code or access token, which an extension can then use to access user data from a service that supports OAuth2 access (such as Google or Facebook). The API provides the `identity.launchWebAuthFlow()` function to handle user authentication and authorization.

OAuth2 flows vary between service providers, so consult their documentation for specific implementation details.

## Permissions
- `identity` - required

## Types
None

## Methods

### getRedirectURL()
Generates a URL that you can use as a redirect URL in OAuth2 flows.

**Syntax**: `browser.identity.getRedirectURL()`

#### Parameters
None

#### Returns
- **Type**: `string`
- **Description**: A redirect URL derived from the extension's ID

**Important Notes**:
- The URL is derived from your extension's ID
- Set your extension's ID explicitly using the `browser_specific_settings` key in manifest.json
- Otherwise, each temporary installation generates a different redirect URL
- Format: Fixed domain with subdomain based on extension ID
- Starting from Firefox 86, loopback addresses are also permitted: `http://127.0.0.1/mozoauth2/[subdomain]`

#### Code Examples
```javascript
let redirectURL = browser.identity.getRedirectURL();
console.log(redirectURL);
// Example output: https://[extension-id].extensions.allizom.org/
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/identity/getRedirectURL

### launchWebAuthFlow()
Performs the first part of an OAuth2 flow, including user authentication and client authorization.

**Syntax**: `browser.identity.launchWebAuthFlow(details)`

#### Parameters
| Name | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `details` | object | Yes | - | Options for the OAuth2 flow |
| `details.url` | string | Yes | - | OAuth2 service provider's authorization URL |
| `details.redirect_uri` | string | No | - | URI for redirection after flow completion |
| `details.interactive` | boolean | No | false | Whether to allow user interaction |

**URL Parameters**: The authorization URL must include:
- `redirect_uri`: The redirect URL (from `getRedirectURL()` or custom)
- `client_id`: Your extension's client ID from the OAuth2 provider
- `response_type`: OAuth2 response type (e.g., "token" or "code")
- `scope`: Requested permissions

**Interactive Mode**:
- `true`: Allows user interaction for sign-in/authorization
- `false` or omitted: Forces silent completion (fails if interaction needed)
- Use `true` when responding to user actions
- Omit for background operations

#### Returns
- **Type**: `Promise<string>`
- **Description**: Fulfilled with redirect URL containing access token or authorization code

**Error Conditions**:
- Service provider URL unreachable
- Client ID mismatch
- Redirect URL not registered
- Authentication failure
- Authorization denied
- User interaction needed but `interactive` was false

#### Code Examples
```javascript
function authorize() {
  const redirectURL = browser.identity.getRedirectURL();
  const clientID = "your-client-id";
  const scopes = ["openid", "email", "profile"];
  
  let authURL = "https://accounts.google.com/o/oauth2/auth";
  authURL += `?client_id=${clientID}`;
  authURL += `&response_type=token`;
  authURL += `&redirect_uri=${encodeURIComponent(redirectURL)}`;
  authURL += `&scope=${encodeURIComponent(scopes.join(" "))}`;
  
  return browser.identity.launchWebAuthFlow({
    interactive: true,
    url: authURL
  });
}

// Usage
authorize()
  .then(responseUrl => {
    // Extract access token from responseUrl
    const url = new URL(responseUrl);
    const params = new URLSearchParams(url.hash.slice(1));
    const accessToken = params.get('access_token');
    console.log('Access token:', accessToken);
  })
  .catch(error => {
    console.error('Authorization failed:', error);
  });
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/identity/launchWebAuthFlow

## Events
None

## Setup Process

### 1. Get Redirect URL
```javascript
const redirectURL = browser.identity.getRedirectURL();
```

### 2. Register with OAuth2 Provider
- Create an application/client on the provider's website
- Supply your redirect URL
- Receive client ID (and sometimes client secret)
- Note allowed redirect URLs

### 3. Set Extension ID (Optional but Recommended)
```json
// manifest.json
{
  "browser_specific_settings": {
    "gecko": {
      "id": "myextension@example.com"
    }
  }
}
```

### 4. Implement OAuth2 Flow
```javascript
async function authenticate() {
  const redirectURL = browser.identity.getRedirectURL();
  const authURL = buildAuthURL(redirectURL, clientId, scopes);
  
  try {
    const responseUrl = await browser.identity.launchWebAuthFlow({
      url: authURL,
      interactive: true
    });
    
    // Process the response URL to extract tokens
    return extractTokenFromUrl(responseUrl);
  } catch (error) {
    console.error('Auth failed:', error);
  }
}
```

## OAuth2 Provider Examples

### Google
- Auth URL: `https://accounts.google.com/o/oauth2/auth`
- Token URL: `https://oauth2.googleapis.com/token`
- Scopes: Use space-separated list

### GitHub
- Auth URL: `https://github.com/login/oauth/authorize`
- Token URL: `https://github.com/login/oauth/access_token`
- Scopes: Use comma-separated list

## Security Considerations

1. **Redirect URL Validation**: Starting Firefox 75, must use the URL returned by `getRedirectURL()` or the loopback address
2. **Client Secrets**: Never include client secrets in extension code
3. **Token Storage**: Store tokens securely using extension storage APIs
4. **Token Refresh**: Implement token refresh logic for long-lived access

## Related APIs
- `storage` - For securely storing OAuth tokens
- `webRequest` - For adding auth headers to requests
- `cookies` - For managing authentication cookies