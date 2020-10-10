
[`net.connect()`][], [`net.createConnection()`][], [`server.listen()`][] 和
[`socket.connect()`][] 使用一个 `path` 参数来识别 IPC 端点。

在 Unix 上，本地域也称为 Unix 域。
参数 `path` 是文件系统路径名。
它会被截断为依赖于系统的 `sizeof(sockaddr_un.sun_path) - 1` 的长度。
典型值在 Linux 上为 107，在 macOS 上为 103。
如果一个 Node.js API 的抽象创建了 Unix 域 socket，则它也可以 unlink 该 Unix 域 socket。
例如，[`net.createServer()`] 可以创建 Unix 域 socket，而 [`server.close()`] 可以 unlink 它。
但是，如果用户在这些抽象之外创建 Unix 域 socket，则用户需要自己删除它。
当 Node.js API 创建 Unix 域 socket 但该程序随后崩溃时，情况也是如此。
简而言之，Unix 域 socket 会在文件系统中可见，且持续到被 unlink。

在 Windows 上，本地域通过命名管道实现。路径必须是以 `\\?\pipe\` 或 `\\.\pipe\` 为入口。路径允许任何字符，但后面的字符可能会对管道名称进行一些处理，例如解析 `..` 序列。尽管如此，管道空间是平面的。管道不会持续，当最后一次引用关闭时，管道就会被删除。

JavaScript 字符串转义需要使用双反斜杠指定路径，例如：

```js
net.createServer().listen(
  path.join('\\\\?\\pipe', process.cwd(), 'myctl'));
```

