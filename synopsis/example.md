
例子，使用 Node.js 编写的 [Web 服务器](http.html)，响应返回 `'Hello World'`：

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
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

要运行这个服务器，需将代码保存到名为 `example.js` 的文件，并使用 Node.js 来执行：

```txt
$ node example.js
Server running at http://127.0.0.1:3000/
```

文档中所有的例子都可以用相同的方式运行。

