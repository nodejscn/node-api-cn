<!-- YAML
changes:
  - version: v12.3.0
    pr-url: https://github.com/nodejs/node/pull/27151
    description: The `'uncaughtException'` event is from now on triggered if the
                 repl is used as standalone program.
-->

REPL 使用 [`domain`] 模块来捕获该 REPL 会话的所有未捕获的异常。

在 REPL 中对 [`domain`] 模块的这种使用具有以下的副作用：

* 未捕获的异常仅在独立的 REPL 中触发 [`'uncaughtException'`] 事件。 
  在另一个 Node.js 程序的 REPL 中添加此事件的监听器会抛出 [`ERR_INVALID_REPL_INPUT`]。
  
* 尝试使用 [`process.setUncaughtExceptionCaptureCallback()`] 会抛出 [`ERR_DOMAIN_CANNOT_SET_UNCAUGHT_EXCEPTION_CAPTURE`] 错误。

作为独立程序：

```js
process.on('uncaughtException', () => console.log('未捕获的异常'));

throw new Error('foobar');
// 未捕获的异常
```

当在另一个应用程序中使用时：

```js
process.on('uncaughtException', () => console.log('未捕获的异常'));
// TypeError [ERR_INVALID_REPL_INPUT]: Listeners for `uncaughtException`
// cannot be used in the REPL

throw new Error('foobar');
// 抛出:
// Error: foobar
```

