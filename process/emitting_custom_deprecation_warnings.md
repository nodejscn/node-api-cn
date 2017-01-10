
Custom deprecation warnings can be emitted by setting the `name` of a custom
warning to `DeprecationWarning`. For instance:

```js
process.emitWarning('This API is deprecated', 'DeprecationWarning');
```

Or,

```js
const err = new Error('This API is deprecated');
err.name = 'DeprecationWarning';
process.emitWarning(err);
```

Launching Node.js using the `--throw-deprecation` command line flag will
cause custom deprecation warnings to be thrown as exceptions.

Using the `--trace-deprecation` command line flag will cause the custom
deprecation to be printed to `stderr` along with the stack trace.

Using the `--no-deprecation` command line flag will suppress all reporting
of the custom deprecation.

The `*-deprecation` command line flags only affect warnings that use the name
`DeprecationWarning`.

