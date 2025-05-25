---
title: chrome.documentScan
url: https://developer.chrome.com/docs/extensions/reference/api/documentScan
---

## Description

Use the `chrome.documentScan` API to discover and retrieve images from attached document scanners.

The Document Scan API is designed to allow apps and extensions to view the content of paper documents on an attached document scanner.

**Important:** This API works only on ChromeOS.

## Permissions

`documentScan`

## Availability

Chrome 44+ ChromeOS only

Availability for API members added later is shown with those members.

## Concepts and usage

This API supports two means of scanning documents. If your use case can work with any scanner and doesn't require control of the configuration, use the `scan()` method. More complicated use cases require a combination of methods, which are only supported in Chrome 124 and later.

### Simple scanning

For simple use cases, meaning those that can work with any scanner and don't require control of configuration, call `scan()`. This method takes a `ScanOptions` object and returns a `Promise` that resolves with a `ScanResults` object. The capabilities of this option are limited to the number of scans and the MIME types that will be accepted by the caller. Scans are returned as URLs for display in an `<img>` tag for a user interface.

### Complex scanning

Complex scans are accomplished in three phases as described in this section. This outline does not describe every method argument or every property returned in a response. It is only intended to give you a general guide to writing scanner code.

**Note:** Calling `openScanner()`, `getScannerList()`, or `startScan()` more than once will cancel operations initiated by previous calls to these methods. See the descriptions of these methods for specifics.

#### Discovery

1.  Call `getScannerList()`. Available scanners are returned in a `Promise` that resolves with a `GetScannerListResponse`.
    *   The response object contains an array of `ScannerInfo` objects.
    *   The array may contain multiple entries for a single scanner if that scanner supports multiple protocols or connection methods.
2.  Select a scanner from the returned array and save the value of its `scannerId` property.
    Use the properties of individual `ScannerInfo` objects to distinguish among multiple objects for the same scanner. Objects from the same scanner will have the same value for the `deviceUuid` property. `ScannerInfo` also contains an `imageFormats` property containing an array of supported image types.

#### Scanner configuration

1.  Call `openScanner()`, passing in the saved scanner ID. It returns a `Promise` that resolves with an `OpenScannerResponse`. The response object contains:
    *   A `scannerHandle` property, which you'll need to save.
    *   An `options` property containing scanner-specific properties, which you'll need to set. See Retrieve scanner options for more information.
2.  (Optional) If you need the user to provide values for scanner options, construct a user interface. You will need the scanner options provided by the previous step, and you'll need to retrieve option groups provided by the scanner. See Construct a user interface for more information.
3.  Construct an array of `OptionSetting` objects using programmatic or user-provided values. See Set scanner options for more information.
4.  Pass the array of `OptionSetting` objects to `setOptions()` to set options for the scanner. It returns a `Promise` that resolves with a `SetOptionsResponse`. This object contains an updated version of the scanner options retrieved in step 1 of scanner configuration.
    Since changing one option can alter constraints on another option, you may need to repeat these steps several times.

#### Scanning

1.  Construct a `StartScanOptions` object and pass it to `startScan()`. It returns a `Promise` that resolves with a `StartScanResponse`. Its `job` property is a handle that you will use to either read scan data or cancel the scan.
2.  Pass the job handle to `readScanData()`. It returns a `Promise` that resolves with a `ReadScanDataResponse` object. If data was read successfully, its `result` property equals `SUCCESS` and its `data` property contains an `ArrayBuffer` with part of the scan. Note that `estimatedCompletion` contains an estimated percentage of the total data that has been delivered so far.
    **Note:** If `result` is `SUCCESS`, but `data` is empty, delay briefly before calling `readScanData()` again.
3.  Repeat the previous step until the `result` property equals `EOF` or an error.

When the end of the scan is reached, call `closeScanner()` with the scanner handle saved in step 3. It returns a `Promise` that resolves with a `CloseScannerResponse`. Calling `cancelScan()` at any time after the job is created will end scanning.

### Response objects

All methods return a `Promise` that resolves with a response object of some kind. Most of these contain a `result` property whose value is a member of `OperationResult`. Some properties of response objects won't contain values unless the value of `result` has a specific value. These relationships are described in the reference for each response object.

For example, `OpenScannerResponse.scannerHandle` will only have a value when `OpenScannerResponse.result` equals `SUCCESS`.

### Scanner options

Scanner options vary considerably by device. Consequently, it's not possible to reflect scanner options directly within the `documentScan` API. To get around this, the `OpenScannerResponse` (retrieved using `openScanner()`) and the `SetOptionsResponse` (the response object for `setOptions()`) contain an `options` property which is an object containing scanner-specific options. Each option is a key-value mapping where the key is a device-specific option and the value is an instance of `ScannerOption`.

The structure generally looks like this:

```
{ "key1": { scannerOptionInstance } "key2": { scannerOptionInstance } }
```

For example, imagine a scanner that returns options named `"source"` and `"resolution"`. The structure of the returned `options` object will look something like the following example. For simplicity, only partial `ScannerOption` responses are shown.

```
{ "source": { "name": "source", "type": OptionType.STRING, ... }, "resolution": { "name": "resolution", "type": OptionType.INT, ... }, ... }
```

### Construct a user interface

Though not required to use this API, you may want a user to choose the value for a particular option. This requires a user interface. Use the `OpenScannerResponse` (opened by `openScanner()`) to retrieve the options for the attached scanner as described in the previous section.

Some scanners group options in device-specific ways. They don't affect option behaviors, but since these groups may be mentioned in a scanner's product documentation, such groups should be shown to the user. You can retrieve these groups by calling `getOptionGroups()`. This returns a `Promise` that resolves with a `GetOptionGroupsResponse` object. Its `groups` property contains a scanner-specific array of groups. Use the information in these groups to organize the options in the `OpenScannerResponse` for display.

```
{ scannerHandle: "123456", result: SUCCESS, groups: [ { title: chrome."Standard", members: [ "resolution", "mode", "source" ] } ] }
```

As stated under Scanner configuration, changing one option can alter constraints on another option. This is why `setOptionsResponse` (the response object for `setOptions()`) contains another `options` property. Use this to update the user interface. Then repeat as needed until all options are set.

### Set scanner options

Set scanner options by passing an array of `OptionSetting` objects to `setOptions()`. For an example, see the following Scan one letter-size page section.

## Examples

### Retrieve a page as a blob

This example shows one way to retrieve a page from the scanner as a blob and demonstrates use of `startScan()` and `readScanData()` using the value of `OperationResult`.

```javascript
async function pageAsBlob(handle) {
  let response = await chrome.documentScan.startScan(
    handle,
    {format: "image/jpeg"});
  if (response.result != chrome.documentScan.OperationResult.SUCCESS) {
    return null;
  }
  const job = response.job;
  let imgParts = [];
  response = await chrome.documentScan.readScanData(job);
  while (response.result == chrome.documentScan.OperationResult.SUCCESS) {
    if (response.data && response.data.byteLength > 0) {
      imgParts.push(response.data);
    } else {
      // Delay so hardware can make progress.
      await new Promise(r => setTimeout(r, 100));
    }
    response = await chrome.documentScan.readScanData(job);
  }
  if (response.result != chrome.documentScan.OperationResult.EOF) {
    return null;
  }
  if (response.data && response.data.byteLength > 0) {
    imgParts.push(response.data);
  }
  return new Blob(imgParts, { type: "image/jpeg" });
}
```

### Scan one letter-size page

This example shows how to select a scanner, set its options, and open it. It then retrieves the contents of a single page and closes the scanner. This process demonstrates using `getScannerList()`, `openScanner()`, `setOptions()`, and `closeScanner()`. Note that the contents of the page are retrieved by calling the `pageAsBlob()` function from the previous example.

```javascript
async function scan() {
  let response = await chrome.documentScan.getScannerList({ secure: true });
  let scanner = await chrome.documentScan.openScanner(
    response.scanners[0].scannerId);
  const handle = scanner.scannerHandle;
  let options = [];
  for (source of scanner.options["source"].constraint.list) {
    if (source.includes("ADF")) {
      options.push({
        name: "source",
        type: chrome.documentScan.OptionType.STRING,
        value: { value: source }
      });
      break;
    }
  }
  options.push({
    name: "tl-x",
    type: chrome.documentScan.OptionType.FIXED,
    value: 0.0
  });
  options.push({
    name: "br-x",
    type: chrome.documentScan.OptionType.FIXED,
    value: 215.9 // 8.5" in mm
  });
  options.push({
    name: "tl-y",
    type: chrome.documentScan.OptionType.FIXED,
    value: 0.0
  });
  options.push({
    name: "br-y",
    type: chrome.documentScan.OptionType.FIXED,
    value: 279.4 // 11" in mm
  });
  response = await chrome.documentScan.setOptions(handle, options);
  let imgBlob = await pageAsBlob(handle);
  if (imgBlob != null) {
    // Insert imgBlob into DOM, save to disk, etc
  }
  await chrome.documentScan.closeScanner(handle);
}
```

### Show the configuration

As stated elsewhere, showing a scanner's configuration options to a user requires calling `getOptionGroups()` in addition to the scanner options returned from a call to `openScanner()`. This is so that options can be shown to users in manufacturer-defined groups. This example shows how to do that.

```javascript
async function showConfig() {
  let response = await chrome.documentScan.getScannerList({ secure: true });
  let scanner = await chrome.documentScan.openScanner(
    response.scanners[0].scannerId);
  let groups = await chrome.documentScan.getOptionGroups(scanner.scannerHandle);
  for (const group of groups.groups) {
    console.log("=== " + group.title + " ===");
    for (const member of group.members) {
      const option = scanner.options[member];
      if (option.isActive) {
        console.log("  " + option.name + " = " + option.value);
      } else {
        console.log("  " + option.name + " is inactive");
      }
    }
  }
}
```

## Types

### `CancelScanResponse`

Chrome 125+

#### Properties

*   `job`

    string

    Provides the same job handle that was passed to `cancelScan()`.
*   `result`

    `OperationResult`

    The backend's cancel scan result. If the result is `OperationResult.SUCCESS` or `OperationResult.CANCELLED`, the scan has been cancelled and the scanner is ready to start a new scan. If the result is `OperationResult.DEVICE_BUSY` , the scanner is still processing the requested cancellation; the caller should wait a short time and try the request again. Other result values indicate a permanent error that should not be retried.

### `CloseScannerResponse`

Chrome 125+

#### Properties

*   `result`

    `OperationResult`

    The result of closing the scanner. Even if this value is not `SUCCESS`, the handle will be invalid and should not be used for any further operations.
*   `scannerHandle`

    string

    The same scanner handle as was passed to `closeScanner`.

### `Configurability`

Chrome 125+

How an option can be changed.

#### Enum

*   `"NOT_CONFIGURABLE"`
    The option is read-only.
*   `"SOFTWARE_CONFIGURABLE"`
    The option can be set in software.
*   `"HARDWARE_CONFIGURABLE"`
    The option can be set by the user toggling or pushing a button on the scanner.

### `ConnectionType`

Chrome 125+

Indicates how the scanner is connected to the computer.

#### Enum

*   `"UNSPECIFIED"`
*   `"USB"`
*   `"NETWORK"`

### `ConstraintType`

Chrome 125+

The data type of constraint represented by an `OptionConstraint`.

#### Enum

*   `"INT_RANGE"`
    The constraint on a range of `OptionType.INT` values. The `min`, `max`, and `quant` properties of `OptionConstraint` will be long, and its `list` propety will be unset.
*   `"FIXED_RANGE"`
    The constraint on a range of `OptionType.FIXED` values. The `min`, `max`, and `quant` properties of `OptionConstraint` will be double, and its `list` property will be unset.
*   `"INT_LIST"`
    The constraint on a specific list of `OptionType.INT` values. The `OptionConstraint.list` property will contain long values, and the other properties will be unset.
*   `"FIXED_LIST"`
    The constraint on a specific list of `OptionType.FIXED` values. The `OptionConstraint.list` property will contain double values, and the other properties will be unset.
*   `"STRING_LIST"`
    The constraint on a specific list of `OptionType.STRING` values. The `OptionConstraint.list` property will contain DOMString values, and the other properties will be unset.

### `DeviceFilter`

Chrome 125+

#### Properties

*   `local`

    boolean optional

    Only return scanners that are directly attached to the computer.
*   `secure`

    boolean optional

    Only return scanners that use a secure transport, such as USB or TLS.

### `GetOptionGroupsResponse`

Chrome 125+

#### Properties

*   `groups`

    `OptionGroup[]` optional

    If `result` is `SUCCESS`, provides a list of option groups in the order supplied by the scanner driver.
*   `result`

    `OperationResult`

    The result of getting the option groups. If the value of this is `SUCCESS`, the `groups` property will be populated.
*   `scannerHandle`

    string

    The same scanner handle as was passed to `getOptionGroups`.

### `GetScannerListResponse`

Chrome 125+

#### Properties

*   `result`

    `OperationResult`

    The enumeration result. Note that partial results could be returned even if this indicates an error.
*   `scanners`

    `ScannerInfo[]`

    A possibly-empty list of scanners that match the provided `DeviceFilter`.

### `OpenScannerResponse`

Chrome 125+

#### Properties

*   `options`

    object optional

    If `result` is `SUCCESS`, provides a key-value mapping where the key is a device-specific option and the value is an instance of `ScannerOption`.
*   `result`

    `OperationResult`

    The result of opening the scanner. If the value of this is `SUCCESS`, the `scannerHandle` and `options` properties will be populated.
*   `scannerHandle`

    string optional

    If `result` is `SUCCESS`, a handle to the scanner that can be used for further operations.
*   `scannerId`

    string

    The scanner ID passed to `openScanner()`.

### `OperationResult`

Chrome 125+

An enum that indicates the result of each operation.

#### Enum

*   `"UNKNOWN"`
    An unknown or generic failure occurred.
*   `"SUCCESS"`
    The operation succeeded.
*   `"UNSUPPORTED"`
    The operation is not supported.
*   `"CANCELLED"`
    The operation was cancelled.
*   `"DEVICE_BUSY"`
    The device is busy.
*   `"INVALID"`
    Either the data or an argument passed to the method is not valid.
*   `"WRONG_TYPE"`
    The supplied value is the wrong data type for the underlying option.
*   `"EOF"`
    No more data is available.
*   `"ADF_JAMMED"`
    The document feeder is jammed.
*   `"ADF_EMPTY"`
    The document feeder is empty.
*   `"COVER_OPEN"`
    The flatbed cover is open.
*   `"IO_ERROR"`
    An error occurred while communicating with the device.
*   `"ACCESS_DENIED"`
    The device requires authentication.
*   `"NO_MEMORY"`
    Not enough memory is available on the Chromebook to complete the operation.
*   `"UNREACHABLE"`
    The device is not reachable.
*   `"MISSING"`
    The device is disconnected.
*   `"INTERNAL_ERROR"`
    An error has occurred somewhere other than the calling application.

### `OptionConstraint`

Chrome 125+

#### Properties

*   `list`

    `string[]` | `number[]` optional
*   `max`

    number optional
*   `min`

    number optional
*   `quant`

    number optional
*   `type`

    `ConstraintType`

### `OptionGroup`

Chrome 125+

#### Properties

*   `members`

    `string[]`

    An array of option names in driver-provided order.
*   `title`

    string

    Provides a printable title, for example "Geometry options".

### `OptionSetting`

Chrome 125+

#### Properties

*   `name`

    string

    Indicates the name of the option to set.
*   `type`

    `OptionType`

    Indicates the data type of the option. The requested data type must match the real data type of the underlying option.
*   `value`

    string | number | boolean | `number[]` optional

    Indicates the value to set. Leave unset to request automatic setting for options that have `autoSettable` enabled. The data type supplied for `value` must match `type`.

### `OptionType`

Chrome 125+

The data type of an option.

#### Enum

*   `"UNKNOWN"`
    The option's data type is unknown. The `value` property will be unset.
*   `"BOOL"`
    The `value` property will be one of `true` or `false`.
*   `"INT"`
    A signed 32-bit integer. The `value` property will be `long` or `long[]`, depending on whether the option takes more than one value.
*   `"FIXED"`
    A double in the range -32768-32767.9999 with a resolution of 1/65535. The `value` property will be `double` or `double[]` depending on whether the option takes more than one value. Double values that can't be exactly represented will be rounded to the available range and precision.
*   `"STRING"`
    A sequence of any bytes except NUL ('\0'). The `value` property will be a DOMString.
*   `"BUTTON"`
    An option of this type has no value. Instead, setting an option of this type causes an option-specific side effect in the scanner driver. For example, a button-typed option could be used by a scanner driver to provide a means to select default values or to tell an automatic document feeder to advance to the next sheet of paper.
*   `"GROUP"`
    Grouping option. No value. This is included for compatibility, but will not normally be returned in `ScannerOption` values. Use `getOptionGroups()` to retrieve the list of groups with their member options.

### `OptionUnit`

Chrome 125+

Indicates the data type for `ScannerOption.unit`.

#### Enum

*   `"UNITLESS"`
    The value is a unitless number. For example, it can be a threshold.
*   `"PIXEL"`
    The value is a number of pixels, for example, scan dimensions.
*   `"BIT"`
    The value is the number of bits, for example, color depth.
*   `"MM"`
    The value is measured in millimeters, for example, scan dimensions.
*   `"DPI"`
    The value is measured in dots per inch, for example, resolution.
*   `"PERCENT"`
    The value is a percent.