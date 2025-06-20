# WebRequest

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webRequest
- **Version**: Firefox WebExtensions API

## Overview

Add event listeners for the various stages of making an HTTP request, which includes websocket requests on `ws://` and `wss://`. The event listener receives detailed information about the request and can modify or cancel the request.

## Permissions
- **Required**: `"webRequest"` API permission and host permissions for relevant hosts
- **Blocking**: `"webRequestBlocking"` API permission for modifying requests
- **Host Permissions**: Required for both main page and resources being intercepted

## Request Lifecycle

### Primary Event Sequence
1. `onBeforeRequest` - Request about to be made, before headers available
2. `onBeforeSendHeaders` - Before sending HTTP data, headers available
3. `onSendHeaders` - Just before sending headers
4. `onHeadersReceived` - Response headers received
5. `onResponseStarted` - First byte of response body received
6. `onCompleted` - Request completed successfully

### Alternative Events
- `onBeforeRedirect` - Server-initiated redirect about to occur
- `onAuthRequired` - Server requests authentication credentials
- `onErrorOccurred` - Error occurs (can fire at any time)

## Types

### RequestFilter
Object describing filters to apply to webRequest events.

| Property | Type | Description |
|----------|------|-------------|
| urls | string[] | URL patterns to match |
| types | ResourceType[] | Resource types to filter |
| tabId | integer | Specific tab ID |
| windowId | integer | Specific window ID |

### ResourceType
| Value | Description |
|-------|-------------|
| `"main_frame"` | Top-level document |
| `"sub_frame"` | Sub-frame document |
| `"stylesheet"` | CSS stylesheet |
| `"script"` | JavaScript |
| `"image"` | Image resource |
| `"font"` | Font resource |
| `"object"` | Plugin object |
| `"xmlhttprequest"` | XMLHttpRequest |
| `"ping"` | Ping request |
| `"csp_report"` | CSP violation report |
| `"media"` | Video/audio |
| `"websocket"` | WebSocket |
| `"other"` | Other resource types |
| `"speculative"` | Speculative connection |

### HttpHeaders
Array of HTTP headers, each with:
| Property | Type | Description |
|----------|------|-------------|
| name | string | Header name |
| value | string | Header value (optional) |
| binaryValue | integer[] | Binary header value (optional) |

### BlockingResponse
Object returned by blocking listeners to modify requests.

| Property | Type | Description |
|----------|------|-------------|
| cancel | boolean | Cancel the request |
| redirectUrl | string | Redirect to different URL |
| requestHeaders | HttpHeaders | Modified request headers |
| responseHeaders | HttpHeaders | Modified response headers |
| authCredentials | object | Authentication credentials |

### SecurityInfo
Object describing TLS security properties.

| Property | Type | Description |
|----------|------|-------------|
| state | string | Security state ("secure", "insecure", "broken") |
| certificates | CertificateInfo[] | Certificate chain |
| weaknessReasons | string[] | Security weakness reasons |

### StreamFilter
Object for monitoring and modifying HTTP response bodies.

| Method | Description |
|--------|-------------|
| write() | Write data to response stream |
| disconnect() | Disconnect from stream |
| close() | Close the stream |
| suspend() | Suspend data processing |
| resume() | Resume data processing |

## Methods

### handlerBehaviorChanged()
**Syntax**: `webRequest.handlerBehaviorChanged()`

Ensures event listeners are applied correctly when pages are in browser's in-memory cache.

#### Returns
- **Type**: `Promise<void>`
- **Description**: Promise that resolves when behavior change is processed

#### Code Examples
```javascript
// Call after modifying request handling behavior
browser.webRequest.handlerBehaviorChanged();
```

### filterResponseData()
**Syntax**: `webRequest.filterResponseData(requestId)`

Returns a StreamFilter object for examining and modifying response data.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| requestId | string | Yes | Request ID from event listener |

#### Returns
- **Type**: `StreamFilter`
- **Description**: Object for filtering response data

#### Code Examples
```javascript
browser.webRequest.onBeforeRequest.addListener(
  (details) => {
    if (details.url.includes("example.com")) {
      const filter = browser.webRequest.filterResponseData(details.requestId);
      
      filter.ondata = (event) => {
        const decoder = new TextDecoder("utf-8");
        const encoder = new TextEncoder();
        let str = decoder.decode(event.data, {stream: true});
        
        // Modify the response
        str = str.replace(/original/g, "modified");
        
        filter.write(encoder.encode(str));
      };
      
      filter.onstop = (event) => {
        filter.close();
      };
    }
  },
  {urls: ["*://example.com/*"]},
  ["blocking"]
);
```

### getSecurityInfo()
**Syntax**: `webRequest.getSecurityInfo(requestId, options)`

Gets detailed TLS connection information for a request.

#### Parameters
| Name | Type | Required | Description |
|------|------|----------|-------------|
| requestId | string | Yes | Request ID |
| options | object | No | Options object |
| options.certificateChain | boolean | No | Include full certificate chain |
| options.rawDER | boolean | No | Include raw DER data |

#### Returns
- **Type**: `Promise<SecurityInfo>`
- **Description**: TLS security information

#### Code Examples
```javascript
browser.webRequest.onHeadersReceived.addListener(
  async (details) => {
    if (details.url.startsWith("https://")) {
      const securityInfo = await browser.webRequest.getSecurityInfo(
        details.requestId,
        {certificateChain: true}
      );
      console.log("Security state:", securityInfo.state);
    }
  },
  {urls: ["<all_urls>"]},
  ["blocking"]
);
```

## Events

### onBeforeRequest
**Fired when**: Request is about to be made, before headers are available

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| requestId | string | Unique request identifier |
| url | string | Target URL |
| method | string | HTTP method |
| frameId | integer | Frame ID (0 for main frame) |
| parentFrameId | integer | Parent frame ID |
| tabId | integer | Tab ID |
| type | ResourceType | Type of resource |
| timeStamp | number | Request timestamp |
| originUrl | string | Origin URL |
| requestBody | object | Request body data (if available) |

#### Code Examples
```javascript
// Block requests to specific domain
browser.webRequest.onBeforeRequest.addListener(
  (details) => {
    if (details.url.includes("blocked-domain.com")) {
      return {cancel: true};
    }
  },
  {urls: ["<all_urls>"]},
  ["blocking"]
);

// Redirect requests
browser.webRequest.onBeforeRequest.addListener(
  (details) => {
    if (details.url.includes("old-domain.com")) {
      return {
        redirectUrl: details.url.replace("old-domain.com", "new-domain.com")
      };
    }
  },
  {urls: ["*://old-domain.com/*"]},
  ["blocking"]
);
```

### onBeforeSendHeaders
**Fired when**: Before sending HTTP data, headers are available

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| requestId | string | Request identifier |
| url | string | Target URL |
| method | string | HTTP method |
| requestHeaders | HttpHeaders | Request headers |
| tabId | integer | Tab ID |
| type | ResourceType | Resource type |

#### Code Examples
```javascript
// Modify request headers
browser.webRequest.onBeforeSendHeaders.addListener(
  (details) => {
    details.requestHeaders.push({
      name: "Custom-Header",
      value: "Custom-Value"
    });
    
    return {requestHeaders: details.requestHeaders};
  },
  {urls: ["*://example.com/*"]},
  ["blocking", "requestHeaders"]
);
```

### onSendHeaders
**Fired when**: Just before sending headers (after modifications)

### onHeadersReceived
**Fired when**: HTTP response headers received

#### Event Properties
| Property | Type | Description |
|----------|------|-------------|
| requestId | string | Request identifier |
| url | string | Target URL |
| statusCode | integer | HTTP status code |
| responseHeaders | HttpHeaders | Response headers |
| statusLine | string | Complete status line |

#### Code Examples
```javascript
// Modify response headers
browser.webRequest.onHeadersReceived.addListener(
  (details) => {
    details.responseHeaders.push({
      name: "Custom-Response-Header",
      value: "Custom-Value"
    });
    
    return {responseHeaders: details.responseHeaders};
  },
  {urls: ["<all_urls>"]},
  ["blocking", "responseHeaders"]
);
```

### onAuthRequired
**Fired when**: Server requests authentication credentials

#### Code Examples
```javascript
browser.webRequest.onAuthRequired.addListener(
  (details) => {
    return {
      authCredentials: {
        username: "user",
        password: "pass"
      }
    };
  },
  {urls: ["*://secure-site.com/*"]},
  ["blocking"]
);
```

### onResponseStarted
**Fired when**: First byte of response body received

### onBeforeRedirect
**Fired when**: Server-initiated redirect about to occur

### onCompleted
**Fired when**: Request completed successfully

### onErrorOccurred
**Fired when**: Error occurs during request

## Request Modification

### Blocking Operations
To modify requests, use `"blocking"` in `extraInfoSpec`:

```javascript
browser.webRequest.onBeforeRequest.addListener(
  (details) => {
    // Return BlockingResponse object
    return {cancel: true}; // or {redirectUrl: "..."} etc.
  },
  {urls: ["<all_urls>"]},
  ["blocking"] // Required for modifications
);
```

### Available Modifications
- **Cancel**: Set `cancel: true`
- **Redirect**: Set `redirectUrl: "new-url"`
- **Modify Headers**: Set `requestHeaders` or `responseHeaders`
- **Authentication**: Set `authCredentials`

### Extra Info Specifications
| Value | Description |
|-------|-------------|
| `"blocking"` | Required for request modification |
| `"requestHeaders"` | Access to request headers |
| `"responseHeaders"` | Access to response headers |
| `"requestBody"` | Access to request body |

## Response Data Filtering

### StreamFilter Usage
```javascript
browser.webRequest.onBeforeRequest.addListener(
  (details) => {
    const filter = browser.webRequest.filterResponseData(details.requestId);
    
    filter.ondata = (event) => {
      // Process event.data
      filter.write(modifiedData);
    };
    
    filter.onstop = () => {
      filter.close();
    };
  },
  {urls: ["*://example.com/*"]},
  ["blocking"]
);
```

## Constants

### MAX_HANDLER_BEHAVIOR_CHANGED_CALLS_PER_10_MINUTES
Maximum number of times `handlerBehaviorChanged()` can be called in 10 minutes.

## Related APIs
- `webNavigation` - Navigation-level events
- `tabs` - Tab management
- `permissions` - Permission management

## Notes
- Based on Chromium's chrome.webRequest API
- Request IDs are unique within browser session and extension context
- Speculative requests have inaccurate tab/frame information
- HSTS upgrades may trigger immediate redirects
- Tracking Protection blocks appear as errors
