<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4557
    description: The default action of calling `.destroy()` on the `socket`
                 will no longer take place if there are listeners attached
                 for `clientError`.
  - version: v8.10.0
    pr-url: https://github.com/nodejs/node/pull/17672
    description: The rawPacket is the current buffer that just parsed. Adding
                 this buffer to the error object of clientError event is to make
                 it possible that developers can log the broken packet.
-->

* `exception` {Error}
* `socket` {net.Socket}

如果客户端触发了一个 `'error'` 事件，则它会被传递到这里。
该事件的监听器负责关闭或销毁底层的 socket。
例如，用户可能希望更温和地用 HTTP `'400 Bad Request'` 响应关闭 socket，而不是突然地切断连接。

默认情况下，请求异常时会立即销毁 socket。

`socket` 参数是发生错误的 [`net.Socket`] 对象。

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

当 `'clientError'` 事件发生时，不会有 `request` 或 `response` 对象，所以发送的任何 HTTP 响应，包括响应头和内容，必须被直接写入到 `socket` 对象。
注意，确保响应是一个被正确格式化的 HTTP 响应消息。

`err` is an instance of `Error` with two extra columns:

+ `bytesParsed`: the bytes count of request packet that Node.js may have parsed
  correctly;
+ `rawPacket`: the raw packet of current request.
