<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}
* `address` {Object}

当一个工作进程调用`listen()`后，工作进程上的server会触发`'listening'` 事件，同时主进程上的 `cluster` 也会被触发`'listening'`事件。

事件处理器使用两个参数来执行，其中`worker`包含了工作进程对象，`address` 包含了以下连接属性： `address`、`port` 和 `addressType`。当工作进程同时监听多个地址时，这些参数非常有用。

```js
cluster.on('listening', (worker, address) => {
  console.log(
    `A worker is now connected to ${address.address}:${address.port}`);
});
```

`addressType` 可选值包括:

* `4` (TCPv4)
* `6` (TCPv6)
* `-1` (unix domain socket)
* `"udp4"` or `"udp6"` (UDP v4 or v6)

