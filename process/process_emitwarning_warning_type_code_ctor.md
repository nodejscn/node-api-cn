<!-- YAML
added: v6.0.0
-->

* `warning` {string|Error} 发出的警告。
* `type` {string} 如果 `warning` 是String, `type` 是警告类型的名字。 默认值: `Warning`。
* `code` {string} 当前警告的唯一标识符。
* `ctor` {Function} 如果`warning`是String，`ctor`是可选的function，用于限制生成的堆栈信息。默认`process.emitWarning`

`process.emitWarning()`方法可用于发出定制的或应用特定的进程警告。
可以通过给[`process.on('warning')`][process_warning]事件增加处理器，监听这些警告。

```js
// Emit a warning using a string.
process.emitWarning('Something happened!');
// Emits: (node: 56338) Warning: Something happened!
```

```js
// Emit a warning using a string and a type.
process.emitWarning('Something Happened!', 'CustomWarning');
// Emits: (node:56338) CustomWarning: Something Happened!
```

```js
process.emitWarning('Something happened!', 'CustomWarning', 'WARN001');
// Emits: (node:56338) [WARN001] CustomWarning: Something happened!
```

在上面例子中，`process.emitWarning()`内部生成了一个`Error`对象，并传递给[`process.on('warning')`][process_warning]事件。

```js
process.on('warning', (warning) => {
  console.warn(warning.name);
  console.warn(warning.message);
  console.warn(warning.code);
  console.warn(warning.stack);
});
```

如果`warning`参数值是一个`Error`对象，它会被透传给`process.on('warning')`的事件监听器(可选参数值`type`，`code` and `ctor`会被忽略)：

```js
// Emit a warning using an Error object.
const myWarning = new Error('Something happened!');
// Use the Error name property to specify the type name
myWarning.name = 'CustomWarning';
myWarning.code = 'WARN001';

process.emitWarning(myWarning);
// Emits: (node:56338) [WARN001] CustomWarning: Something happened!
```

如果`warning`的参数值不是string或`Error`，会抛出 `TypeError`。

需要注意的是，使用`Error`对象做为进程警告，**并不是**常用的错误处理机制的替代方式。

如果警告`type`是`DeprecationWarning`，会涉及如下额外的处理：

* 如果命令行标识包含`--throw-deprecation`，deprecation warning会作为异常抛出，而不是作为事件被发出。

* 如果命令行标识包含`--no-deprecation`，deprecation warning会被忽略。

* 如果命令行标识包含`--trace-deprecation`，deprecation warning及其全部堆栈信息会被打印到`stderr`。

