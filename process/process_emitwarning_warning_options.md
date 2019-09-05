<!-- YAML
added: v8.0.0
-->

* `warning` {string|Error} 触发的警告。
* `options` {Object}
  * `type` {string} 当 `warning` 是一个 `String` 时，则 `type` 是用于被触发的警告类型的名称。 **默认值:** `'Warning'`。
  * `code` {string} 要触发的警告实例的唯一标识符。
  * `ctor` {Function} 当 `warning` 是一个 `String` 时，则 `ctor` 是一个可选的函数，用于限制生成的堆栈信息。**默认值:** `process.emitWarning`。
  * `detail` {string} 错误的附加信息。

`process.emitWarning()` 方法可用于触发自定义或应用特定的进程警告。
可以通过给 [`'warning'`][process_warning] 事件增加处理程序来监听这些警告。

```js
// 使用代码和其他详细信息触发警告。
process.emitWarning('出错啦', {
  code: 'MY_WARNING',
  detail: '一些额外的信息'
});
// 触发:
// (node:56338) [MY_WARNING] Warning: 出错啦
// 一些额外的信息
```

在上面例子中，`process.emitWarning()` 内部生成了一个 `Error` 对象，并传给 [`'warning'`][process_warning] 句柄。

```js
process.on('warning', (warning) => {
  console.warn(warning.name);    // 'Warning'
  console.warn(warning.message); // '出错啦'
  console.warn(warning.code);    // 'MY_WARNING'
  console.warn(warning.stack);   // Stack trace
  console.warn(warning.detail);  // '一些额外的信息'
});
```

如果 `warning` 是一个 `Error` 对象，则 `options` 参数会被忽略。

