<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4557
    description: The default action of calling `.destroy()` on the `socket`
                 will no longer take place if there are listeners attached
                 for `'clientError'`.
  - version: v9.4.0
    pr-url: https://github.com/nodejs/node/pull/17672
    description: The `rawPacket` is the current buffer that just parsed. Adding
                 this buffer to the error object of `'clientError'` event is to
                 make it possible that developers can log the broken packet.
-->

* `exception` {Error}
* `socket` {net.Socket}

如果客户端连接触发 `'error'` 事件，则会在此处转发。
此事件的监听器负责关闭或销毁底层套接字。
例如，用户可能希望使用自定义 HTTP 响应更优雅地关闭套接字，而不是突然切断连接。

默认行为是尽可能使用 HTTP `400 Bad Request` 响应关闭套接字，否则立即销毁套接字。

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

当 `'clientError'` 事件发生时，没有 `request` 或 `response` 对象，因此必须将发送的任何 HTTP 响应（包括响应头和有效负载）直接写入 `socket` 对象。
必须注意确保响应是格式正确的 HTTP 响应消息。

`err` 是 `Error` 实例，有以下两个额外的部分：

+ `bytesParsed`: Node.js 可能正确解析的请求包的字节数。
+ `rawPacket`: 当前请求的原始数据包。


