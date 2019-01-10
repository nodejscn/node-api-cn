<!-- YAML
added: v0.3.0
-->

* {net.Socket}

指向底层的 socket。
通常不需要访问该属性。
由于协议解析器绑定到 socket 的方式，socket 不会触发`'readable'`事件。
也可以通过 `request.connection` 访问 `socket`。

例子：

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
  console.log(`你的 IP 地址是 ${ip}，端口是 ${port}`);
  // 消费响应对象。
});
```
