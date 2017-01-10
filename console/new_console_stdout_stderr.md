
Creates a new `Console` by passing one or two writable stream instances.
`stdout` is a writable stream to print log or info output. `stderr`
is used for warning or error output. If `stderr` isn't passed, warning and error
output will be sent to `stdout`.

```js
const output = fs.createWriteStream('./stdout.log');
const errorOutput = fs.createWriteStream('./stderr.log');
// custom simple logger
const logger = new Console(output, errorOutput);
// use it like console
var count = 5;
logger.log('count: %d', count);
// in stdout.log: count 5
```

The global `console` is a special `Console` whose output is sent to
[`process.stdout`][] and [`process.stderr`][]. It is equivalent to calling:

```js
new Console(process.stdout, process.stderr);
```

