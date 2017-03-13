<!-- YAML
added: v0.1.99
-->

* `msg` {Buffer} - 消息
* `rinfo` {Object} - 远程地址信息

当有新的数据包被 socket 接收时，`'message'`事件会被触发。`msg`和`rinfo`会作为参数传递到该事件的处理函数中。`msg`参数是一个 [`Buffer`][]，`rinfo`参数是一个提供了发送者地址信息的对象，包含`address`、`family`和`port`属性：

```js
socket.on('message', (msg, rinfo) => {
  console.log('收到来自 %s:%d 的 %d bytes 数据\n',
              msg.length, rinfo.address, rinfo.port);
});
```

