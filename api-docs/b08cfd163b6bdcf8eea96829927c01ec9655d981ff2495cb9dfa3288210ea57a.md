
`path` 模块会因操作系统的差异而不同。
比如在 Windows 上，`path` 模块会认为使用的是 Windows 风格的路径。

例如，对文件路径 `C:\temp\myfile.html` 使用 `path.basename()`，在 POSIX 上与在 Windows 上会产生不同的结果：

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

如果想在任何操作系统上处理 POSIX 文件路径时获得一致的结果，则使用 [`path.posix`]：

在 POSIX 和 Windows 上:

```js
path.posix.basename('/tmp/myfile.html');
// 返回: 'myfile.html'
```

