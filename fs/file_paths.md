
大多数 `fs` 操作接受的文件路径可以指定为字符串、[`Buffer`]、或 [`URL`] 对象（使用 `file:` 协议）。

字符串形式的路径会被解释为 UTF-8 字符序列（标识绝对或相对的文件名）。 
相对路径会相对于当前工作目录（通过调用 `process.cwd()` 确定）进行处理。

在 POSIX 上使用绝对路径的示例：

```js
const fs = require('fs');

fs.open('/文件.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

在 POSIX 上使用相对路径（相对于 `process.cwd()`）的示例：

```js
fs.open('文件.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

使用 [`Buffer`] 指定的路径主要用于将文件路径视为不透明字节序列的某些 POSIX 操作系统。 
在这些系统上，单个文件路径可以包含使用多种字符编码的子序列。 
与字符串路径一样，`Buffer` 路径也可以是相对或绝对的：

在 POSIX 上使用绝对路径的示例：

```js
fs.open(Buffer.from('/文件.txt'), 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

在 Windows 上，Node.js 遵循独立驱动器工作目录的概念。
当使用没有反斜杠的驱动器路径时，可以观察到此行为。
例如，`fs.readdirSync('C:\\')` 可能会返回与 `fs.readdirSync('C:')` 不同的结果。
详见[此 MSDN 页面][MSDN-Rel-Path]。

