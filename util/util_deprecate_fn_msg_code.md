<!-- YAML
added: v0.8.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/16393
    description: Deprecation warnings are only emitted once for each code.
-->

* `fn` {Function} The function that is being deprecated.
* `msg` {string} A warning message to display when the deprecated function is
  invoked.
* `code` {string} A deprecation code. See the [list of deprecated APIs][] for a
  list of codes.
* Returns: {Function} The deprecated function wrapped to emit a warning.

The `util.deprecate()` method wraps `fn` (which may be a function or class) in
such a way that it is marked as deprecated.

```js
const util = require('util');

exports.obsoleteFunction = util.deprecate(() => {
  // Do something here.
}, 'obsoleteFunction() is deprecated. Use newShinyFunction() instead.');
```

When called, `util.deprecate()` will return a function that will emit a
`DeprecationWarning` using the [`'warning'`][] event. The warning will
be emitted and printed to `stderr` the first time the returned function is
called. After the warning is emitted, the wrapped function is called without
emitting a warning.

If the same optional `code` is supplied in multiple calls to `util.deprecate()`,
the warning will be emitted only once for that `code`.

```js
const util = require('util');

const fn1 = util.deprecate(someFunction, someMessage, 'DEP0001');
const fn2 = util.deprecate(someOtherFunction, someOtherMessage, 'DEP0001');
fn1(); // emits a deprecation warning with code DEP0001
fn2(); // does not emit a deprecation warning because it has the same code
```

If either the `--no-deprecation` or `--no-warnings` command line flags are
used, or if the `process.noDeprecation` property is set to `true` *prior* to
the first deprecation warning, the `util.deprecate()` method does nothing.

If the `--trace-deprecation` or `--trace-warnings` command line flags are set,
or the `process.traceDeprecation` property is set to `true`, a warning and a
stack trace are printed to `stderr` the first time the deprecated function is
called.

If the `--throw-deprecation` command line flag is set, or the
`process.throwDeprecation` property is set to `true`, then an exception will be
thrown when the deprecated function is called.

The `--throw-deprecation` command line flag and `process.throwDeprecation`
property take precedence over `--trace-deprecation` and
`process.traceDeprecation`.

