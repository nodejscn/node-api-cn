<!-- YAML
changes:
  - version: v12.3.0
    pr-url: https://github.com/nodejs/node/pull/27151
    description: The `'uncaughtException'` event is from now on triggered if the
                 repl is used as standalone program.
-->

REPL使用 [`domain`] 模块来捕获会话期间的所有未捕获异常。

在REPL中使用 [`domain`] 模块有如下副作用：

* 如果将 `repl` 用作独立程序，则未捕获的异常仅触发 [`'uncaughtException'`] 事件。 
  如果 `repl` 包含在另一个应用程序的任何位置，则为此事件添加监听器将会抛出 [`ERR_INVALID_REPL_INPUT`] 异常。
* 如果尝试使用 [`process.setUncaughtExceptionCaptureCallback()`] 将产生一个 [`ERR_DOMAIN_CANNOT_SET_UNCAUGHT_EXCEPTION_CAPTURE`] 错误。

作为独立程序：

```js
process.on('uncaughtException', () => console.log('未捕获的异常'));

throw new Error('foobar');
// 打印：未捕获的异常
```

当在其他应用程序中使用时：

```js
process.on('uncaughtException', () => console.log('未捕获的异常'));
// 抛出 TypeError [ERR_INVALID_REPL_INPUT]: Listeners for `uncaughtException` cannot be used in the REPL

throw new Error('foobar');
// 抛出:
// Error: foobar
```

