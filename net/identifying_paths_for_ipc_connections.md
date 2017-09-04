
[`net.connect()`][], [`net.createConnection()`][], [`server.listen()`][] and
[`socket.connect()`][] take a `path` parameter to identify IPC endpoints.


[`net.connect()`][], [`net.createConnection()`][], [`server.listen()`][] 和
[`socket.connect()`][] 使用 `path` 参数来识别 IPC 端点。

在 UNIX 上，本地域也称为 UNIX 域。参数 `path` 是文件系统路径名。它被从 `sizeof(sockaddr_un.sun_path) - 1` 处被截断，其长度因操作系统不同而在 91 至 107 字节之间变化。典型值在 Linux 上为 107，在 macOS 上为 103。该路径受到与创建文件相同的命名约定和权限检查。它将在文件系统中可见，并且将持续到取消链接的时候。

在 Windows 上，本地域通过命名管道实现。路径必须是以 `\\?\pipe\` 或 `\\.\pipe\` 为入口。路径允许任何字符，但后面的字符可能会对管道名称进行一些处理，例如解析 `..` 序列。尽管如此，管道空间是平面的。管道不会持续，当最后一次引用关闭时，管道就会被删除。不要忘了 JavaScript 字符串转义需要使用双反斜杠指定路径，例如：

```js
net.createServer().listen(
  path.join('\\\\?\\pipe', process.cwd(), 'myctl'));
```

