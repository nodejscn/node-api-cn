
<!--type=misc-->

大多数 Node.js 核心 API 所提供的异步方法都遵从错误信息优先的回调模式惯例，这种模式有时也称为 Node.js 式回调。在这种模式中，一个回调函数首先被作为参数传给异步方法。当该方法完成操作或产生错误时，它会调用回调函数，并将可能存在的 `Error` 对象作为第一个参数传给回调函数。如果没有错误产生，那么第一个参数为 `null` 。

```js
const fs = require('fs');

function errorFirstCallback(err, data) {
  if (err) {
    console.error('There was an error', err);
    return;
  }
  console.log(data);
}

fs.readFile('/some/file/that/does-not-exist', errorFirstCallback);
fs.readFile('/some/file/that/does-exist', errorFirstCallback);
```

JavaScript的 `try / catch` 机制**不能**用来截获异步方法产生的错误。新手的常见错误之一是试图在错误优先回调函数中使用 `throw` ：
```js
// 这不可行：
const fs = require('fs');

try {
  fs.readFile('/some/file/that/does-not-exist', (err, data) => {
    // mistaken assumption: throwing here...
    if (err) {
      throw err;
    }
  });
} catch (err) {
  // 这里不会截获回调函数中的throw
  console.error(err);
}
```

这样做不可行，因为传递给 `fs.readFile()` 的回调函数是异步调用的。当回调函数被调用时，程序早已退出其周围的代码（包括 `try { } catch (err) { }` 部分）。在回调函数内抛出异常在大多数时候**会使 Node.js 进程崩溃**。但如果启用了 [domains][] ，或者有与 `process.on('uncaughtException')` 相关联的异常处理器，就可以截获这种错误。

