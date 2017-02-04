
> 稳定性: 2 - 稳定的

<!--name=fs-->

文件 I/O 是由简单封装的标准 POSIX 函数提供的。
通过 `require('fs')` 使用该模块。
所有的方法都有异步和同步的形式。

异步形式始终以完成回调作为它最后一个参数。
传给完成回调的参数取决于具体方法，但第一个参数总是留给异常。
如果操作成功完成，则第一个参数会是 `null` 或 `undefined`。

当使用同步形式时，任何异常都会被立即抛出。
可以使用 try/catch 来处理异常，或让它们往上冒泡。

这是异步版本的例子：

```js
const fs = require('fs');

fs.unlink('/tmp/hello', (err) => {
  if (err) throw err;
  console.log('successfully deleted /tmp/hello');
});
```

这是同步版本的例子：

```js
const fs = require('fs');

fs.unlinkSync('/tmp/hello');
console.log('successfully deleted /tmp/hello');
```

异步方法不保证执行顺序。
所以下面的例子容易出错：

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  console.log('renamed complete');
});
fs.stat('/tmp/world', (err, stats) => {
  if (err) throw err;
  console.log(`stats: ${JSON.stringify(stats)}`);
});
```

`fs.stat` 可能在 `fs.rename` 之前执行。正确的方法是把回调链起来。

```js
fs.rename('/tmp/hello', '/tmp/world', (err) => {
  if (err) throw err;
  fs.stat('/tmp/world', (err, stats) => {
    if (err) throw err;
    console.log(`stats: ${JSON.stringify(stats)}`);
  });
});
```

在繁忙的进程中，**强烈推荐**开发者使用这些函数的异步版本。
同步版本会阻塞整个进程，直到它们完成（停止所有连接）。

可使用文件名的相对路径。
但该路径是相对 `process.cwd()` 的。

大部分 fs 函数会让你忽略回调参数。
如果你这么做，一个默认的回调将用于抛出错误。
为了追踪原始的调用点，可设置 `NODE_DEBUG` 环境变量：

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

