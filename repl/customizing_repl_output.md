
默认情况下，`repl.REPLServer` 实例使用 [`util.inspect()`] 方法，在输出结果信息到指定的输出流（默认`process.stdout`）之前，设置输出的格式。
使用 `util.inspect()` 方法，可以设置布尔量选项 `useColors`，在建立默认输出器的时候指定是否使用 ANSI 风格给代码上色。

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

