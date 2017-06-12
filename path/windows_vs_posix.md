
`path` 模块的默认操作会根据 Node.js 应用程序运行的操作系统的不同而变化。
比如，当运行在 Windows 操作系统上时，`path` 模块会认为使用的是 Windows 风格的路径。

例如，对 Windows 文件路径 `C:\temp\myfile.html` 使用 `path.basename()` 函数，运行在 POSIX 上与运行在 Windows 上会产生不同的结果：

在 POSIX 上:

```js
path.basename('C:\\temp\\myfile.html');
// 返回: 'C:\\temp\\myfile.html'
```

在 Windows 上:

```js
path.basename('C:\\temp\\myfile.html');
// 返回: 'myfile.html'
```

要想在任何操作系统上处理 Windows 文件路径时获得一致的结果，可以使用 [`path.win32`]：

在 POSIX 和 Windows 上:

```js
path.win32.basename('C:\\temp\\myfile.html');
// 返回: 'myfile.html'
```

要想在任何操作系统上处理 POSIX 文件路径时获得一致的结果，可以使用 [`path.posix`]：

在 POSIX 和 Windows 上:

```js
path.posix.basename('/tmp/myfile.html');
// 返回: 'myfile.html'
```

注意：在 Windows 上 Node.js 遵循单驱动器工作目录的理念。
当使用驱动器路径且不带反斜杠时就能体验到该特征。
例如，`fs.readdirSync('c:\\')` 可能返回与 `fs.readdirSync('c:')` 不同的结果。
详见 [MSDN 路径文档]。

