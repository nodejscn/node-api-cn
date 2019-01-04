
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

<!--name=fs-->

`fs` 模块提供了一个 API，用于以接近标准 POSIX 函数的方式与文件系统进行交互。

要使用此模块：

```js
const fs = require('fs');
```

所有文件系统操作都具有同步和异步的形式。

异步的形式始终将完成回调作为其最后一个参数。
传递给完成回调的参数取决于具体方法，但第一个参数始终保留用于异常。
如果操作成功完成，则第一个参数将为 `null` 或 `undefined`。

```js
const fs = require('fs');

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('已成功删除 /tmp/hello');
});
```

使用同步操作发生的异常会立即抛出，可以使用 `try`/`catch` 处理，也可以允许冒泡。

```js
const fs = require('fs');

try {
  fs.unlinkSync('/tmp/hello');
  console.log('已成功删除 /tmp/hello');
} catch (err) {
  // 处理错误
}
```

使用异步方法时无法保证顺序。
因此，以下的例子容易出错，因为 `fs.stat()` 操作可能在 `fs.rename()` 操作之前完成：


```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  console.log('重命名完成');
});
fs.stat('/tmp/world', (err, stats) => {
  if (err) throw err;
  console.log(`文件属性: ${JSON.stringify(stats)}`);
});
```

要想按正确的顺序执行操作，请将 `fs.stat()` 操作移动到 `fs.rename()` 操作的回调中：

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  });
});
```

在繁忙的进程中，强烈建议使用这些操作的异步版本。
同步版本将阻塞整个进程，直到它们完成。

虽然不推荐这样使用，但大多数 `fs` 函数允许省略回调参数，在这种情况下，使用默认的回调。
要跟踪原始的调用点，请设置 `NODE_DEBUG` 环境变量：

建议不要在异步 `fs` 函数上省略回调函数，因为可能导致将来抛出错误。


```txt
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

