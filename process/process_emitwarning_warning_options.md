<!-- YAML
added: 8.0.0
-->

* `warning` {string|Error} The warning to emit.
* `options` {Object}
  * `type` {string} When `warning` is a String, `type` is the name to use
    for the *type* of warning being emitted. Default: `Warning`.
  * `code` {string} A unique identifier for the warning instance being emitted.
  * `ctor` {Function} When `warning` is a String, `ctor` is an optional
    function used to limit the generated stack trace. Default
    `process.emitWarning`
  * `detail` {string} Additional text to include with the error.

The `process.emitWarning()` method can be used to emit custom or application
specific process warnings. These can be listened for by adding a handler to the
[`process.on('warning')`][process_warning] event.

```js
// Emit a warning with a code and additional detail.
process.emitWarning('Something happened!', {
  code: 'MY_WARNING',
  detail: 'This is some additional information'
});
// Emits:
// (node:56338) [MY_WARNING] Warning: Something happened!
// This is some additional information
```

In this example, an `Error` object is generated internally by
`process.emitWarning()` and passed through to the
[`process.on('warning')`][process_warning] event.

```js
process.on('warning', (warning) => {
  console.warn(warning.name);    // 'Warning'
  console.warn(warning.message); // 'Something happened!'
  console.warn(warning.code);    // 'MY_WARNING'
  console.warn(warning.stack);   // Stack trace
  console.warn(warning.detail);  // 'This is some additional information'
});
```

If `warning` is passed as an `Error` object, the `options` argument is ignored.

