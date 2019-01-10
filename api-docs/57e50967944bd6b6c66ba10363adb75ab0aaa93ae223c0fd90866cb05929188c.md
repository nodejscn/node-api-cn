
默认情况下，在把输出写入到提供的可写流（默认为 `process.stdout`）之前，`repl.REPLServer` 实例会使用 [`util.inspect()`] 方法对输出进行格式化。
使用 `util.inspect()` 方法时，`useColors` 选项可被指定是否在建立默认输出器时使用 ANSI 风格的代码给输出上色。

在构造时，通过在 `writer` 选项传入一个新的函数，可以完全地自定义一个 `repl.REPLServer` 实例的输出。
例子，把输入的任何文本转换为大写：

```js
const repl = require('repl');

const r = repl.start({ prompt: '> ', eval: myEval, writer: myWriter });

function myEval(cmd, context, filename, callback) {
  callback(null, cmd);
}

function myWriter(output) {
  return output.toUpperCase();
}
```

