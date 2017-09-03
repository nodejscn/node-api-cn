<!-- YAML
added: v0.1.91
changes:
  - version: v5.8.0
    pr-url: https://github.com/nodejs/node/pull/5388
    description: The `options` parameter is optional now.
-->

* `options` {Object|string}
  * `prompt` {string} 要显示的输入提示符。默认为 `> `（末尾有一个空格）。
  * `input` {Readable} REPL 输入要被读取的可读流。默认为 `process.stdin`。
  * `output` {Writable} REPL 输出要被写入的可写流。默认为 `process.stdout`。
  * `terminal` {boolean} 如果为 `true`，则指定 `output` 应被当作一个 TTY 终端，并且可以使用 ANSI/VT100 转义码写入。
    默认值为初始化时 `output` 流的 `isTTY` 属性的值。
  * `eval` {Function} 当解释每行输入时使用的函数。默认为 JavaScript `eval()` 函数的异步封装。
    `eval` 函数出错时会返回 `repl.Recoverable`，表明输入不完整并提示用户完成输入。
  * `useColors` {boolean} 如果为 `true`，则指定默认的 `writer` 函数可以在 REPL 输出中包含 ANSI 颜色风格。
    如果提供了自定义的 `writer` 函数，则该参数无效。
    默认为 REPL 实例的 `terminal` 属性的值。
  * `useGlobal` {boolean} 如果为 `true`，则指定默认的解释函数使用 JavaScript `global` 作为上下文，而不是为 REPL 实例创建一个新的独立的上下文。
    The node CLI REPL sets this value to `true`.
    默认为 `false`。
  * `ignoreUndefined` {boolean} 如果为 `true`，则指定默认的输出器不会输出命令返回的 `undefined` 值。
     默认为 `false`。
  * `writer` {Function} 在写入到 `output` 之前，该函数被调用用来格式化每个命令的输出。
    默认为 [`util.inspect()`]。
  * `completer` {Function} 可选的函数，用来自定义 Tab 键的自动补全。
    详见 [`readline.InterfaceCompleter`]。
  * `replMode` {symbol} 一个标志位，指定默认的解释器使用严格模式或默认（sloppy）模式来执行 JavaScript 命令。
    可选的值有：
    * `repl.REPL_MODE_SLOPPY` - 使用默认模式解释表达式。
    * `repl.REPL_MODE_STRICT` - 使用严格模式解释表达式。该模式等同于在每个 repl 声明前加上 `'use strict'`。
    * `repl.REPL_MODE_MAGIC` - This value is **deprecated**, since enhanced
      spec compliance in V8 has rendered magic mode unnecessary. It is now
      equivalent to `repl.REPL_MODE_SLOPPY` (documented above).
  * `breakEvalOnSigint` - 当接收到 `SIGINT` 时停止解释当前代码，比如按下 `Ctrl+C`。
    不能与自定义的 `eval` 函数同时使用。
    默认为 `false`。

`repl.start()` 方法创建并启动一个 `repl.REPLServer` 实例。

如果 `options` 是一个字符串，则它指定了输入提示符：

```js
const repl = require('repl');

// 一个 Unix 风格的提示符
repl.start('$ ');
```

