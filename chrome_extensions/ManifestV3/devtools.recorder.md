---
title: chrome.devtools.recorder
url: https://developer.chrome.com/docs/extensions/reference/api/devtools/recorder
---

## Description

Use the `chrome.devtools.recorder` API to customize the Recorder panel in DevTools.

`devtools.recorder` API is a preview feature that allows you to extend the Recorder panel in Chrome DevTools.

See DevTools APIs summary for general introduction to using Developer Tools APIs.

## Availability

Chrome 105+

Starting from Chrome 105, you can extend the export functionality. Starting from Chrome 112, you can extend the replay button.

## Concepts and usage

### Customizing the export feature

To register an extension plugin, use the `registerRecorderExtensionPlugin` function. This function requires a plugin instance, a `name` and a `mediaType` as parameters. The plugin instance must implement two methods: `stringify` and `stringifyStep`.

The `name` provided by the extension shows up in the Export menu in the Recorder panel.

Depending on the export context, when the user clicks the export option provided by the extension, the Recorder panel invokes one of the two functions:

*   `stringify` that receives an entire user flow recording
*   `stringifyStep` that receives a single recorded step

The `mediaType` parameter allows the extension to specify the kind of output it generates with the `stringify` and `stringifyStep` functions. For example, `application/javascript` if the result is a JavaScript program.

### Customizing the replay button

To customize the replay button in the Recorder, use the `registerRecorderExtensionPlugin` function. The plugin must implement the `replay` method for the customization to take effect. If the method is detected, a replay button will appear in the Recorder. Upon clicking the button, the current recording object will be passed as the first argument to the `replay` method.

At this point, the extension can display a `RecorderView` for handling the replay or use other extension APIs to process the replay request. To create a new `RecorderView`, invoke `chrome.devtools.recorder.createView`.

## Examples

### Export plugin

The following code implements an extension plugin that stringifes a recording using `JSON.stringify`:

```javascript
class MyPlugin {
  stringify(recording) {
    return Promise.resolve(JSON.stringify(recording));
  }
  stringifyStep(step) {
    return Promise.resolve(JSON.stringify(step));
  }
}
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  new MyPlugin(),
  /*name=*/'MyPlugin',
  /*mediaType=*/'application/json'
);
```

### Replay plugin

The following code implements an extension plugin that creates a dummy Recorder view and displays it upon a replay request:

```javascript
const view = await chrome.devtools.recorder.createView(
  /* name= */ 'ExtensionName',
  /* pagePath= */ 'Replay.html'
);
let latestRecording;
view.onShown.addListener(() => {
  // Recorder has shown the view. Send additional data to the view if needed.
  chrome.runtime.sendMessage(JSON.stringify(latestRecording));
});
view.onHidden.addListener(() => {
  // Recorder has hidden the view.
});
export class RecorderPlugin {
  replay(recording) {
    // Share the data with the view.
    latestRecording = recording;
    // Request to show the view.
    view.show();
  }
}
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  new RecorderPlugin(),
  /* name=*/ 'CoffeeTest'
);
```

Find a complete extension example on GitHub.

## Types

### RecorderExtensionPlugin

A plugin interface that the Recorder panel invokes to customize the Recorder panel.

#### Properties

*   `replay`

    `void`

    Chrome 112+

    Allows the extension to implement custom replay functionality.

    The `replay` function looks like:

    ```javascript
    (recording: object) => {...}
    ```

    *   `recording`

        `object`

        A recording of the user interaction with the page. This should match Puppeteer's recording schema.
*   `stringify`

    `void`

    Converts a recording from the Recorder panel format into a string.

    The `stringify` function looks like:

    ```javascript
    (recording: object) => {...}
    ```

    *   `recording`

        `object`

        A recording of the user interaction with the page. This should match Puppeteer's recording schema.
*   `stringifyStep`

    `void`

    Converts a step of the recording from the Recorder panel format into a string.

    The `stringifyStep` function looks like:

    ```javascript
    (step: object) => {...}
    ```

    *   `step`

        `object`

        A step of the recording of a user interaction with the page. This should match Puppeteer's step schema.

### RecorderView

Chrome 112+

Represents a view created by extension to be embedded inside the Recorder panel.

#### Properties

*   `onHidden`

    `Event<functionvoidvoid>`

    Fired when the view is hidden.

    The `onHidden.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `onShown`

    `Event<functionvoidvoid>`

    Fired when the view is shown.

    The `onShown.addListener` function looks like:

    ```javascript
    (callback: function) => {...}
    ```

    *   `callback`

        `function`

        The callback parameter looks like:

        ```javascript
        () => void
        ```
*   `show`

    `void`

    Indicates that the extension wants to show this view in the Recorder panel.

    The `show` function looks like:

    ```javascript
    () => {...}
    ```

## Methods

### createView()

Chrome 112+

```javascript
chrome.devtools.recorder.createView(
  title: chrome.string,
  pagePath: string,
)
```

Creates a view that can handle the replay. This view will be embedded inside the Recorder panel.

#### Parameters

*   `title`

    `string`

    Title that is displayed next to the extension icon in the Developer Tools toolbar.
*   `pagePath`

    `string`

    Path of the panel's HTML page relative to the extension directory.

#### Returns

*   `RecorderView`

### registerRecorderExtensionPlugin()

```javascript
chrome.devtools.recorder.registerRecorderExtensionPlugin(
  plugin: RecorderExtensionPlugin,
  name: string,
  mediaType: string,
)
```

Registers a Recorder extension plugin.

#### Parameters

*   `plugin`

    `RecorderExtensionPlugin`

    An instance implementing the `RecorderExtensionPlugin` interface.
*   `name`

    `string`

    The name of the plugin.
*   `mediaType`

    `string`

    The media type of the string content that the plugin produces.