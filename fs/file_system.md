
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

<!--name=fs-->

`fs` 模块提供了用于与文件系统进行交互（以类似于标准 POSIX 函数的方式）的 API。

要使用此模块：

```js
const fs = require('fs');
```

所有的文件系统操作都具有同步和异步的形式。

异步的形式总是把完成回调作为其最后一个参数。
传给完成回调的参数取决于具体方法，但第一个参数总是预留给异常。
如果操作被成功地完成，则第一个参数会为 `null` 或 `undefined`。

```js
const fs = require('fs');

fs.unlink('文件', (err) => {
  if (err) throw err;
  console.log('已成功地删除文件');
});
```

当使用同步的操作时，发生的异常会被立即地抛出，可以使用 `try…catch` 处理，也可以冒泡。

```js
const fs = require('fs');

try {
  fs.unlinkSync('文件');
  console.log('已成功地删除文件');
} catch (err) {
  // 处理错误
}
```

当使用异步的方法时，无法保证顺序。
因此，以下的操作容易出错，因为 `fs.stat()` 操作可能在 `fs.rename()` 操作之前完成：


```js
fs.rename('旧文件', '新文件', (err) => {
  if (err) throw err;
  console.log('重命名完成');
});
fs.stat('新文件', (err, stats) => {
  if (err) throw err;
  console.log(`文件属性: ${JSON.stringify(stats)}`);
});
```

若要正确地排序这些操作，则移动 `fs.stat()` 调用到 `fs.rename()` 操作的回调中：

```js
fs.rename('旧文件', '新文件', (err) => {
  if (err) throw err;
  fs.stat('新文件', (err, stats) => {
    if (err) throw err;
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  });
});
```

在繁忙的进程中，应使用这些调用的异步版本。
同步的版本会阻塞整个进程（停止所有的连接），直到它们完成。

虽然不建议这样做，但是大多数 fs 函数都可以省略回调参数，在这种情况下，会使用默认的回调来抛出错误。
若要获取对原始调用点的跟踪，则设置 `NODE_DEBUG` 环境变量：

不建议省略异步的 fs 函数上的回调函数，因为将来可能会抛出错误。


```console
$ cat script.js
function bad() {
  require('fs').readFile('/');
}
bad();

$ env NODE_DEBUG=fs node script.js
fs.js:88
        throw backtrace;
        ^
Error: EISDIR: illegal operation on a directory, read
    <stack trace.>
```

