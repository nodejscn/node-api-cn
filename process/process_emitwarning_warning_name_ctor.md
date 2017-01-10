<!-- YAML
added: v6.0.0
-->

* `warning` {String | Error} The warning to emit.
* `name` {String} When `warning` is a String, `name` is the name to use
  for the warning. Default: `Warning`.
* `ctor` {Function} When `warning` is a String, `ctor` is an optional
  function used to limit the generated stack trace. Default
  `process.emitWarning`

The `process.emitWarning()` method can be used to emit custom or application
specific process warnings. These can be listened for by adding a handler to the
[`process.on('warning')`][process_warning] event.

```js
// Emit a warning using a string...
process.emitWarning('Something happened!');
// Emits: (node: 56338) Warning: Something happened!
```

```js
// Emit a warning using a string and a name...
process.emitWarning('Something Happened!', 'CustomWarning');
// Emits: (node:56338) CustomWarning: Something Happened!
```

In each of the previous examples, an `Error` object is generated internally by
`process.emitWarning()` and passed through to the
[`process.on('warning')`][process_warning] event.

```js
process.on('warning', (warning) => {
  console.warn(warning.name);
  console.warn(warning.message);
  console.warn(warning.stack);
});
```

If `warning` is passed as an `Error` object, it will be passed through to the
`process.on('warning')` event handler unmodified (and the optional `name`
and `ctor` arguments will be ignored):

```js
// Emit a warning using an Error object...
const myWarning = new Error('Warning! Something happened!');
myWarning.name = 'CustomWarning';

process.emitWarning(myWarning);
// Emits: (node:56338) CustomWarning: Warning! Something Happened!
```

A `TypeError` is thrown if `warning` is anything other than a string or `Error`
object.

Note that while process warnings use `Error` objects, the process warning
mechanism is **not** a replacement for normal error handling mechanisms.

The following additional handling is implemented if the warning `name` is
`DeprecationWarning`:

* If the `--throw-deprecation` command-line flag is used, the deprecation
  warning is thrown as an exception rather than being emitted as an event.
* If the `--no-deprecation` command-line flag is used, the deprecation
  warning is suppressed.
* If the `--trace-deprecation` command-line flag is used, the deprecation
  warning is printed to `stderr` along with the full stack trace.

