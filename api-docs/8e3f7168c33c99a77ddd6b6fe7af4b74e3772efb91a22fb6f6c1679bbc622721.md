<!-- YAML
added: v0.3.0
-->

* {net.Socket}

指向底层套接字。 
通常用户无需访问此属性。 
特别是，由于协议解析器附加到套接字的方式，套接字将不会触发 `'readable'` 事件。 
也可以通过 `request.connection` 访问 `socket`。


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
  console.log(`您的 IP 地址是 ${ip}，源端口是 ${port}`);
  // 使用响应对象。
});
```
