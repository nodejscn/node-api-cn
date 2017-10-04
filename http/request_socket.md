<!-- YAML
added: v0.3.0
-->

* {net.Socket}

引用底层socket。 通常用户不想访问此属性。 特别地，由于协议解析器连接到socket的方式，socket将不会触发`'readable'`事件。 在`response.end()`之后，该属性为null。 也可以通过`request.connection`来访问`socket`。

例如:

```js
const http = require('http');
const options = {
  host: 'nodejs.cn',
};
const req = http.get(options);
req.end();
req.once('response', (res) => {
  const ip = req.socket.localAddress;
  const port = req.socket.localPort;
  console.log(`你的IP地址是 ${ip}，你的源端口是 ${port}。`);
  // consume response object
});
```
