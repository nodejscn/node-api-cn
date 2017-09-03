
例子，一个使用 Node.js 编写的 [web服务器]，响应返回 `'Hello World'`：

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`服务器运行在 http://${hostname}:${port}/`);
});
```

要运行这个服务器，需将代码保存到一个名为 `example.js` 的文件，并使用 Node.js 执行：

```txt
$ node example.js
服务器运行在 http://127.0.0.1:3000/
```

文档中所有例子都可以用类似的方法运行。

