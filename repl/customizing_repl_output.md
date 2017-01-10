
By default, `repl.REPLServer` instances format output using the
[`util.inspect()`][] method before writing the output to the provided Writable
stream (`process.stdout` by default). The `useColors` boolean option can be
specified at construction to instruct the default writer to use ANSI style
codes to colorize the output from the `util.inspect()` method.

It is possible to fully customize the output of a `repl.REPLServer` instance
by passing a new function in using the `writer` option on construction. The
following example, for instance, simply converts any input text to upper case:

```js
const repl = require('repl');

const r = repl.start({prompt: '>', eval: myEval, writer: myWriter});

function myEval(cmd, context, filename, callback) {
  callback(null,cmd);
}

function myWriter(output) {
  return output.toUpperCase();
}
```

