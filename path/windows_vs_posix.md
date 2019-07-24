
`path` 模块的默认操作因 Node.js 应用程序运行所在的操作系统而异。
具体来说，当在 Windows 操作系统上运行时，`path` 模块将假定正在使用 Windows 风格的路径。

因此，使用 `path.basename()` 可能会在 POSIX 和 Windows 上产生不同的结果：

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

要在任何操作系统上使用 Windows 文件路径时获得一致的结果，则使用 [`path.win32`]：

在 POSIX 和 Windows 上:

```js
path.win32.basename('C:\\temp\\myfile.html');
// 返回: 'myfile.html'
```

要在任何操作系统上使用 POSIX 文件路径时获得一致的结果，则使用 [`path.posix`]：

在 POSIX 和 Windows 上:

```js
path.posix.basename('/tmp/myfile.html');
// 返回: 'myfile.html'
```

在 Windows 上，Node.js 遵循每个驱动器工作目录的概念。
当使用没有反斜杠的驱动器路径时，可以观察到此行为。
例如，`path.resolve('c:\\')` 可能会返回与 `path.resolve('c:')` 不同的结果。
有关详细信息，参阅[此 MSDN 页面][MSDN-Rel-Path]。

