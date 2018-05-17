<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: The `ignoreErrors` option was introduced.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/19372
    description: The `Console` constructor now supports an `options` argument,
                 and the `colorMode` option was introduced.
-->

* `options` {Object}
  * `stdout` {stream.Writable}
  * `stderr` {stream.Writable}
  * `ignoreErrors` {boolean} Ignore errors when writing to the underlying
                             streams. **Default:** `true`.
  * `colorMode` {boolean|string} Set color support for this `Console` instance.
    Setting to `true` enables coloring while inspecting values, setting to
    `'auto'` will make color support depend on the value of the `isTTY` property
    and the value returned by `getColorDepth()` on the respective stream.
    **Default:** `'auto'`.

Creates a new `Console` with one or two writable stream instances. `stdout` is a
writable stream to print log or info output. `stderr` is used for warning or
error output. If `stderr` is not provided, `stdout` is used for `stderr`.

```js
const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// custom simple logger
const logger = new Console({ stdout: output, stderr: errorOutput });
// use it like console
const count = 5;
logger.log('count: %d', count);
// in stdout.log: count 5
```

The global `console` is a special `Console` whose output is sent to
[`process.stdout`][] and [`process.stderr`][]. It is equivalent to calling:

```js
new Console({ stdout: process.stdout, stderr: process.stderr });
```

