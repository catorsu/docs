# proxy

## Metadata
- **Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/proxy
- **Version**: Current as of June 2025

## Overview

Use the proxy API to proxy web requests. You can use the proxy.onRequest event listener to intercept web requests, and return an object that describes whether and how to proxy them. The advantage is that the proxy policy code runs in your extension's background script with full access to WebExtension APIs.

Note: The "proxy" permission requires "strict_min_version" to be set to "91.1.0" or above. Chrome/Edge/Opera have a different "proxy" API that is incompatible, so this API is only available through the `browser` namespace.

## Permissions
- `proxy` - required to use this API
- Host permissions for URLs you want to intercept

## Types

### ProxyInfo
Describes a proxy server configuration with the following properties:
- **type**: string - "direct", "http", "https", "socks", "socks4" 
- **host**: string - Hostname or IP address of proxy server
- **port**: number - Port number for proxy server
- **username**: string - Username for proxy authentication (SOCKS)
- **password**: string - Password for proxy authentication (SOCKS)
- **proxyDNS**: boolean - Whether proxy performs DNS resolution (SOCKS)
- **failoverTimeout**: number - Failover timeout in seconds
- **proxyAuthorizationHeader**: string - Authorization header for HTTP/HTTPS proxies

### RequestDetails
Contains information about a web request the browser is about to make, including:
- **requestId**: string - Unique request identifier
- **url**: string - Target URL of the request
- **method**: string - HTTP method (GET, POST, etc.)
- **frameId**: number - ID of frame making the request
- **parentFrameId**: number - ID of parent frame (-1 if none)
- **tabId**: number - ID of tab making request (-1 if not from tab)
- **type**: string - Resource type (main_frame, sub_frame, script, etc.)
- **timeStamp**: number - Time when request was made

## Properties

### settings
**Type**: `BrowserSetting<object>`

Get and set proxy settings. Requires private browsing window access since proxy settings affect both private and non-private windows.

#### Setting Properties
| Property | Type | Description |
|----------|------|-------------|
| proxyType | string | "none", "autoDetect", "system", "manual", "autoConfig" |
| http | string | HTTP proxy server (host:port) |
| httpAll | string | HTTP proxy for all protocols |
| ssl | string | HTTPS proxy server |
| socks | string | SOCKS proxy server |
| socksVersion | number | SOCKS version (4 or 5) |
| passthrough | string | Bypass proxy for these hosts |
| autoConfigUrl | string | URL for PAC script |
| autoLogin | boolean | Auto-login to proxy with saved credentials |
| proxyDNS | boolean | Proxy DNS when using SOCKS |

#### Code Examples
```javascript
let proxySettings = {
  proxyType: "manual",
  http: "http://proxy.org:8080",
  socksVersion: 4,
  passthrough: ".example.org",
};

browser.proxy.settings.set({ value: proxySettings });
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/proxy/settings#examples

## Events

### onRequest
**Fired when**: A web request is about to be made, giving the extension an opportunity to proxy it.

This event is fired before any webRequest events for the same request. The listener returns a ProxyInfo object or array of ProxyInfo objects.

#### Listener Function
```javascript
browser.proxy.onRequest.addListener(
  listener,      // function
  filter,        // RequestFilter object  
  extraInfoSpec  // optional array of strings
)
```

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| listener | function | Called when event fires, receives RequestDetails object |
| filter | object | RequestFilter controlling which requests fire the event |
| extraInfoSpec | array | Extra options like "requestHeaders" |

#### Code Examples
```javascript
function shouldProxyRequest(requestInfo) {
  return requestInfo.parentFrameId !== -1;
}

function handleProxyRequest(requestInfo) {
  if (shouldProxyRequest(requestInfo)) {
    console.log(`Proxying: ${requestInfo.url}`);
    return {
      type: "http",
      host: "127.0.0.1", 
      port: 65535
    };
  }
  return { type: "direct" };
}

browser.proxy.onRequest.addListener(handleProxyRequest, {
  urls: ["<all_urls>"]
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/proxy/onRequest#examples

### onError
**Fired when**: The system encounters an error running the PAC script or the onRequest listener.

The error can be triggered by throwing or returning an invalid value in the proxy.onRequest event handler.

#### Parameters
| Name | Type | Description |
|------|------|-------------|
| error | Error | An Error object representing the error |

#### Code Examples
```javascript
browser.proxy.onError.addListener((error) => {
  console.error(`Proxy error: ${error.message}`);
});
```
**Source**: https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/proxy/onError#examples

## Related APIs
- `webRequest` - For more detailed request interception and modification
- `browserSettings.proxyConfig` - Alternative for configuring global proxy settings
- `dns` - For DNS resolution that may be used with proxy configurations
- `storage` - For storing proxy configuration data
