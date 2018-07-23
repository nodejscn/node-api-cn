
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!--name=fs-->

`fs` 模块提供了一些 API，用于以一种类似标准 POSIX 函数的方式与文件系统进行交互。

用法如下：

```js
const fs = require('fs');
```

所有的文件系统操作都有异步和同步两种形式。

异步形式的最后一个参数都是完成时回调函数。
传给回调函数的参数取决于具体方法，但回调函数的第一个参数都会保留给异常。
如果操作成功完成，则第一个参数会是 `null` 或 `undefined`。

```js
const fs = require('fs');

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('成功删除 /tmp/hello');
});
```

当使用同步操作时，任何异常都会被立即抛出，可以使用 `try`/`catch` 来处理异常，或让异常向上冒泡。

```js
const fs = require('fs');

try {
  fs.unlinkSync('/tmp/hello');
  console.log('successfully deleted /tmp/hello');
} catch (err) {
  // handle the error
}
```

异步的方法不能保证执行顺序。
所以下面的例子可能会出错，因为 `fs.stat()` 操作可能在 `fs.rename()` 操作之前完成：

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

若想按正确的顺序执行操作，则需要把 `fs.stat()` 放到 `fs.rename()` 操作的回调函数中：

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  });
});
```

在繁忙的进程中，建议使用函数的异步版本。
同步的方法会阻塞整个进程，直到完成（停止所有连接）。

大多数 fs 函数可以省略回调函数，在这种情况下，会使用默认的回调函数。
若要追踪最初的调用点，可设置 `NODE_DEBUG` 环境变量：

不建议省略异步函数的回调函数，未来的版本可能会导致抛出错误。

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

