
例子，一个使用 Node.js 编写的 [web服务器]，响应返回 `'Hello World'`：

新建一个名为 `hello-world.js` 的源代码文件。

在任何文本编辑器中打开 `hello-world.js`，并将以下内容粘贴进去。

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World!\n');
});

server.listen(port, hostname, () => {
  console.log(`服务器运行在 http://${hostname}:${port}/`);
});
```

保存文件，在终端输入以下命令：

```console
$ node hello-world.js
```

终端中会输出以下内容，表明 Node.js 服务器正在运行：


```console
服务器运行在 http://127.0.0.1:3000/
```

打开浏览器并访问 `http://127.0.0.1:3000`。

如果浏览器显示 `Hello, world!`，则表明服务器正在工作。

文档中大部分例子都可以用类似的方法运行。

