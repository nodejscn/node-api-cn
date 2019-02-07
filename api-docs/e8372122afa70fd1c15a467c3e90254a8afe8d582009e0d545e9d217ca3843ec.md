
大多数 `fs` 操作接受的文件路径可以指定为字符串、[`Buffer`]、或使用 `file:` 协议的 [`URL`] 对象。

字符串形式的路径被解析为标识绝对或相对文件名的 UTF-8 字符序列。 
相对路径将相对于 `process.cwd()` 指定的当前工作目录进行解析。

在 POSIX 上使用绝对路径的示例：

```js
const fs = require('fs');

fs.open('/open/some/file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

在 POSIX 上使用相对路径（相对于 `process.cwd()`）的示例：

```js
fs.open('file.txt', 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

使用 [`Buffer`] 指定的路径主要用于将文件路径视为不透明字节序列的某些 POSIX 操作系统。 
在这样的系统上，单个文件路径可以包含使用多种字符编码的子序列。 
与字符串路径一样，`Buffer` 路径可以是相对路径或绝对路径：

在 POSIX 上使用绝对路径的示例：

```js
fs.open(Buffer.from('/open/some/file.txt'), 'r', (err, fd) => {
  if (err) throw err;
  fs.close(fd, (err) => {
    if (err) throw err;
  });
});
```

在 Windows 上，Node.js 遵循每个驱动器工作目录的概念。
当使用没有反斜杠的驱动器路径时，可以观察到此行为。
例如，`fs.readdirSync('c:\\')` 可能会返回与 `fs.readdirSync('c:')` 不同的结果。
有关详细信息，参阅[此 MSDN 页面][MSDN-Rel-Path]。

