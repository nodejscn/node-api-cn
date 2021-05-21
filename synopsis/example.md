
一个使用 Node.js 编写的响应 `'你好，世界'` 的一个 [web 服务器][web server]的示例：

本文档中的命令以 `$` 或者 `>` 开头，以复制它们怎么出现在一个用户的终端中。
不要包含 `$` 和 `>` 字符。
它们在那里是为了展示每个命令的开头。

不以 `$` 或者 `>` 字符开头的行展示前一个命令的输出。

首先，确保已经下载并且安装 Node.js。
查看[通过包管理器安装 Node.js][Installing Node.js via package manager] 获取更多的安装信息。

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

接下来，在 `projects` 文件夹中创建一个新的源文件，并且命名其为 `hello-world.js`。

在任何首选的文本编辑器中打开 `hello-world.js`，并且粘贴以下的内容：

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

保存文件，返回到终端窗口，并且输入以下的命令：

```console
$ node hello-world.js
```

类似这样的输出应该出现在终端中：

```console
服务器运行在 http://127.0.0.1:3000/
```

现在，打开任何首选的 web 浏览器，并且访问 `http://127.0.0.1:3000`。

如果该浏览器显示字符串 `你好，世界`，则表明该服务器正在工作。

