<!-- YAML
added: v6.0.0
-->

* `warning` {string|Error} 触发的警告。
* `type` {string} 当 `warning` 是一个 `String` 时，则 `type` 是用于被触发的警告类型的名称。 **默认值:** `'Warning'`。
* `code` {string} 要触发的警告实例的唯一标识符。
* `ctor` {Function} 当 `warning` 是一个 `String` 时，则 `ctor` 是一个可选的函数，用于限制生成的堆栈信息。**默认值:** `process.emitWarning`。

`process.emitWarning()` 方法可用于触发自定义或应用特定的进程警告。
可以通过给 [`'warning'`][process_warning] 事件增加处理程序来监听这些警告。

```js
// 使用字符串触发警告。
process.emitWarning('出错啦');
// 触发: (node: 56338) Warning: 出错啦
```

```js
// 使用字符串和类型触发警告。
process.emitWarning('出错啦', 'CustomWarning');
// 触发: (node:56338) CustomWarning: 出错啦
```

```js
process.emitWarning('出错啦', 'CustomWarning', 'WARN001');
// 触发: (node:56338) [WARN001] CustomWarning: 出错啦
```

在前面的每个示例中，`process.emitWarning()` 内部生成了一个 `Error` 对象，并传给 [`'warning'`][process_warning] 句柄。

```js
process.on('warning', (warning) => {
  console.warn(warning.name);
  console.warn(warning.message);
  console.warn(warning.code);
  console.warn(warning.stack);
});
```

如果 `warning` 是一个 `Error` 对象，则它将会被透传给 `'warning'` 事件处理程序（并且将会忽略可选的 `type`、`code` 和 `ctor` 参数）：

```js
// 使用错误对象触发警告。
const myWarning = new Error('出错啦');
// 使用错误名称属性指定类型名称。
myWarning.name = 'CustomWarning';
myWarning.code = 'WARN001';

process.emitWarning(myWarning);
// 触发: (node:56338) [WARN001] CustomWarning: 出错啦
```

如果 `warning` 不是一个字符串或 `Error`，则会抛出 `TypeError`。

当进程警告使用 `Error` 对象时，进程警告机制并不是常用的错误处理机制的替代方式。

如果警告的 `type` 是 `'DeprecationWarning'`，则会涉及如下额外的处理：

* 如果使用 `--throw-deprecation` 命令行标识，则弃用的警告会作为异常抛出，而不是作为事件被触发。
* 如果使用`--no-deprecation` 命令行标识，则弃用的警告会被忽略。
* 如果使用`--trace-deprecation` 命令行标识，则弃用的警告及其全部堆栈信息会被打印到 `stderr`。

