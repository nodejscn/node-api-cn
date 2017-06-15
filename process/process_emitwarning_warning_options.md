<!-- YAML
added: 8.0.0
-->

* `warning` {string|Error} 发出的警告。
* `options` {Object}
  * `type` {string} 如果 `warning` 是String, `type` 是警告类型的名字。 默认值: `Warning`。
  * `code` {string} 当前警告的唯一标识符。
  * `ctor` {Function} 如果`warning`是String，`ctor`是可选的function，用于限制生成的堆栈信息。默认`process.emitWarning`
  * `detail` {string} error的附加信息。

`process.emitWarning()`方法可用于发出定制的或应用特定的进程警告。
可以通过给[`process.on('warning')`][process_warning]事件增加处理器，监听这些警告。

```js
// Emit a warning with a code and additional detail.
process.emitWarning('Something happened!', {
  code: 'MY_WARNING',
  detail: 'This is some additional information'
});
// Emits:
// (node:56338) [MY_WARNING] Warning: Something happened!
// This is some additional information
```

在上面例子中，`process.emitWarning()`内部生成了一个`Error`对象，并传递给[`process.on('warning')`][process_warning]事件。

```js
process.on('warning', (warning) => {
  console.warn(warning.name);    // 'Warning'
  console.warn(warning.message); // 'Something happened!'
  console.warn(warning.code);    // 'MY_WARNING'
  console.warn(warning.stack);   // Stack trace
  console.warn(warning.detail);  // 'This is some additional information'
});
```

如果`warning`参数值是一个`Error`对象，`options`参数项都会被忽略。

