<!-- YAML
added: v0.3.0
-->

* {net.Socket}

引用底层socket。 通常用户不想访问此属性。 特别地，由于协议解析器连接到socket的方式，socket将不会发出`'readable'`事件。 在`response.end()`之后，该属性为null。 也可以通过`response.connection`来访问`socket`。

例如:

```js
const http = require('http');
const server = http.createServer((req, res) => {
  const ip = req.socket.remoteAddress;
  const port = req.socket.remotePort;
  res.end(`你的IP地址是${ip}，你的源端口是${port}.`);
}).listen(3000);
```

