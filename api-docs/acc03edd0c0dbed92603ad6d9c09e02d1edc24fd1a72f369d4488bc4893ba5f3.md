<!-- YAML
added: v0.3.0
-->

* {net.Socket}

指向底层的套接字。 
通常用户不需要访问此属性。 
特别是，由于协议解析器附加到套接字的方式，套接字将不会触发 `'readable'` 事件。 
在调用 `response.end()` 之后，此属性将为空。 
也可以通过 `response.connection` 访问 `socket`。


```js
const http = require('http');
const server = http.createServer((req, res) => {
  const ip = res.socket.remoteAddress;
  const port = res.socket.remotePort;
  res.end(`您的 IP 地址是 ${ip}，您的源端口是 ${port}`);
}).listen(3000);
```

