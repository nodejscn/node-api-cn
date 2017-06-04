<!-- YAML
added: v0.11.14
-->

* `options` {Object} - 必要的。包含以下属性：
  * `port` {number} - 可选的。
  * `address` {string} - 可选的。
  * `exclusive` {boolean} - 可选的。
* `callback` {Function} - 可选的。

对于 UDP socket，该方法会令`dgram.Socket`在指定的`port`和可选的`address`上监听数据包信息。若`port`未指定或为 `0`，操作系统会尝试绑定一个随机的端口。若`address`未指定，操作系统会尝试在所有地址上监听。绑定完成时会触发一个`'listening'`事件，并会调用`callback`方法。

Note that specifying both a `'listening'` event listener and passing a
`callback` to the `socket.bind()` method is not harmful but not very
useful.

在配合[`cluster`]模块使用`dgram.Socket`对象时，`options`对象可能包含一个附加的`exclusive`属性。当`exclusive`被设为`false`(默认值)时，集群工作单元会使用相同的 socket 句柄来共享连接处理作业。当`exclusive`被设为`true`时，该句柄将不会被共享，而尝试共享端口则会造成错误。

A bound datagram socket keeps the Node.js process running to receive
datagram messages.

If binding fails, an `'error'` event is generated. In rare case (e.g.
attempting to bind with a closed socket), an [`Error`][] may be thrown.

一个不共享端口的 socket 的例子如下文所示。


```js
socket.bind({
  address: 'localhost',
  port: 8000,
  exclusive: true
});
```

