<!-- YAML
added: v0.3.0
-->

* {net.Socket}

指向底层的 socket。
通常不需要访问该属性。
由于协议解析器绑定到 socket 的方式，socket 不会触发`'readable'`事件。
调用 `response.end()` 之后，该属性会变为 null。 
也可以通过 `response.connection` 来访问 `socket`。

例子：

```js
const http = require('http');
const server = http.createServer((req, res) => {
  const ip = res.socket.remoteAddress;
  const port = res.socket.remotePort;
  console.log(`你的 IP 地址是 ${ip}，端口是 ${port}`);
}).listen(3000);
```

