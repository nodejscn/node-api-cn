
<!--type=misc-->

大多数由 Node.js 核心 API 暴露出来的异步方法都遵循一个被称为“Node.js 风格的回调”的惯用模式。
使用这种模式，一个回调函数是作为一个参数传给方法的。
当操作完成或发生错误时，回调函数会被调用，并带上错误对象（如果有）作为第一个参数。
如果没有发生错误，则第一个参数为 `null`。


```js
const fs = require('fs');

function nodeStyleCallback(err, data) {
  if (err) {
    console.error('There was an error', err);
    return;
  }
  console.log(data);
}

fs.readFile('/some/file/that/does-not-exist', nodeStyleCallback);
fs.readFile('/some/file/that/does-exist', nodeStyleCallback);
```

JavaScript 的 `try / catch` 机制无法用于捕获由异步 API 引起的错误。
尝试使用 `throw` 而不是一个 Node.js 风格的回调，是初学者常犯的错误：


```js
// 这无法使用：
const fs = require('fs');

try {
  fs.readFile('/some/file/that/does-not-exist', (err, data) => {
    // 假设的错误：在这里抛出
    if (err) {
      throw err;
    }
  });
} catch (err) {
  // 这不会捕获到抛出！
  console.error(err);
}
```

这无法使用，因为传给 `fs.readFile()` 的回调函数是被异步地调用。
当回调被调用时，周围的代码（包括 `try { } catch (err) { }` 区域）已经退出。
大多数情况下，在回调内抛出一个错误会使 Node.js 进程崩溃。
如果[域]已启用，或已在 `process.on('uncaughtException')` 注册了一个句柄，则这些错误可被捕获。

