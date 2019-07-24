
默认情况下，在把输出写入到提供的可写流（默认为 `process.stdout`）之前，[`repl.REPLServer`] 实例会使用 [`util.inspect()`] 方法对输出进行格式化。
`showProxy` 检查选项会默认设置为 true，`colors` 选项会设置为 true，具体取决于 REPL 的 `useColors` 选项。

可以在构造时指定 `useColors` 布尔值选项，以指示默认的编写器使用 ANSI 样式代码来着色来自 `util.inspect()` 方法的输出。

如果 REPL 作为独立程序运行，则还可以使用 `inspect.replDefaults` 属性从 REPL 内部更改 REPL 的检查默认值[`util.inspect()`]，该属性是 [`util.inspect()`] 中的 `defaultOptions` 的镜像。

```console
> util.inspect.replDefaults.compact = false;
false
> [1]
[
  1
]
>
```

在构造时，通过在 `writer` 选项传入一个新的函数，可以完全地自定义一个 [`repl.REPLServer`] 实例的输出。
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

