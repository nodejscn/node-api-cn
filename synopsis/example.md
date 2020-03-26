
一个使用 Node.js 编写的 [web 服务器][web server]的示例，响应返回 `'你好，世界'`：

本文档中的命令以 `$` 或 `>` 开头，以复现它们在用户终端中的显示方式。
实际使用时不用包含 `$` 和 `>` 字符。
它们用于展示每个命令的开始。

不以 `$` 或 `>` 字符开头的命令行展示的是上一个命令的输出。

首先，确保已经下载并安装了 Node.js。
关于安装的更多信息，请参阅[此指南][this guide]。

现在，创建一个空的名为 `projects` 的项目文件夹，然后导航到它。

在 Linux 和 Mac 上：

```console
$ mkdir ~/projects
$ cd ~/projects
```

在 Windows CMD 上：

```console
> mkdir %USERPROFILE%\projects
> cd %USERPROFILE%\projects
```

在 Windows PowerShell 上：

```console
> mkdir $env:USERPROFILE\projects
> cd $env:USERPROFILE\projects
```

接下来，在 `projects` 文件夹中创建一个新的源文件，并将其命名为 `hello-world.js`。

在任何首选的文本编辑器中打开 `hello-world.js` 并粘贴以下内容：

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('你好，世界\n');
});

server.listen(port, hostname, () => {
  console.log(`服务器运行在 http://${hostname}:${port}/`);
});
```

保存文件，返回终端窗口，然后输入以下命令：

```console
$ node hello-world.js
```

终端中会输出以下内容：


```console
服务器运行在 http://127.0.0.1:3000/
```

现在，打开任何首选的 web 浏览器并访问 `http://127.0.0.1:3000`。

如果浏览器显示字符串 `你好，世界`，则表明服务器正在运行。

