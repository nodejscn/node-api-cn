
> 稳定性: 2 - 稳定的

<!--name=fs-->

文件 I/O 是对标准 POSIX 函数的简单封装。
通过 `require('fs')` 使用该模块。
所有的方法都有异步和同步的形式。

异步方法的最后一个参数都是一个回调函数。
传给回调函数的参数取决于具体方法，但回调函数的第一个参数都会保留给异常。
如果操作成功完成，则第一个参数会是 `null` 或 `undefined`。

当使用同步方法时，任何异常都会被立即抛出。
可以使用 `try`/`catch` 来处理异常，或让异常向上冒泡。

异步方法的例子：

```js
const fs = require('fs');

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('成功删除 /tmp/hello');
});
```

同步方法的例子：

```js
const fs = require('fs');

fs.unlinkSync('/tmp/hello');
console.log('成功删除 /tmp/hello');
```

异步的方法不能保证执行顺序。
所以下面的例子可能会出错：

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

`fs.stat` 可能在 `fs.rename` 之前执行。
正确的方法是把回调链起来。

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`文件属性: ${JSON.stringify(stats)}`);
  });
});
```

在繁忙的进程中，建议使用异步的方法。
同步的方法会阻塞整个进程，直到完成（停止所有连接）。

可以使用文件名的相对路径。
路径是相对 `process.cwd()` 的。

大多数 fs 函数可以省略回调函数，在这种情况下，会使用默认的回调函数。
若要追踪最初的调用点，可设置 `NODE_DEBUG` 环境变量：

注意：不建议省略异步方法的回调函数，未来的版本可能会导致抛出错误。

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

注意：在 Windows 上 Node.js 遵循单驱动器工作目录的理念。
当使用驱动器路径且不带反斜杠时就能体验到该特征。
例如，`fs.readdirSync('c:\\')` 可能返回与 `fs.readdirSync('c:')` 不同的结果。
详见 [MSDN 路径文档]。

