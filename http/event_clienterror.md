<!-- YAML
added: v0.1.94
-->

* `exception` {Error}
* `socket` {net.Socket}

如果一个客户端触发了一个 `'error'` 事件，则它会被传递到这里。
该事件的监听器会负责关闭/销毁底层的 socket。
例如，可能希望更温和地用一个 HTTP `'400 Bad Request'` 响应关闭 socket，而不是突然地切断连接。

默认行为是请求异常是立即销毁 socket。

`socket` 是发生错误的 [`net.Socket`] 对象。

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.end();
});
server.on('clientError', (err, socket) => {
  socket.end('HTTP/1.1 400 Bad Request\r\n\r\n');
});
server.listen(8000);
```

当 `'clientError'` 事件发生是，不会有 `request` 或 `response` 对象，所以发送的任何 HTTP 响应，包括响应头和内容，**必须**被直接写入到 `socket` 对象。
必须小心确保响应是一个被正确格式化的 HTTP 响应消息。

