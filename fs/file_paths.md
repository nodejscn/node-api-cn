
大部分 `fs` 操作接受字符串、[`Buffer`]、或使用 `file:` 协议的 [`URL`] 对象作为文件路径。

字符串形式的路径会被解释为表示绝对路径或相对路径的 UTF-8 字符序列。
相对路径会相对于 `process.cwd()` 定义的当前工作目录进行处理。

使用绝对路径的例子：

```js
const fs = require('fs');

fs.open('/open/some/file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

使用相对路径的例子（相对于 `process.cwd()`）：

```js
fs.open('file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

使用 [`Buffer`] 定义的路径主要用于将文件路径处理为 opaque 字节序列的特定 POSIX 操作系统。
在这种系统上，一个文件路径可能包含使用多种字符编码的子序列。
与字符串路径一样，`Buffer` 路径也可以是相对的或绝对的。

使用绝对路径的例子：

```js
fs.open(Buffer.from('/open/some/file.txt'), 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

在 Windows 上，Node.js 遵循 per-drive 工作目录的理念。
当使用驱动器路径不带反斜杠时可以观察到该特性。
例如，`fs.readdirSync('c:\\')` 可能会返回与 `fs.readdirSync('c:')` 不同的结果。
详见 [MSDN路径文档][MSDN-Rel-Path]。

