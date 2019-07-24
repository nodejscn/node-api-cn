<!-- YAML
added: v0.7.0
-->

* `worker` {cluster.Worker}
* `address` {Object}

当一个工作进程调用 `listen()` 后，工作进程上的 server 会触发 `'listening'` 事件，同时主进程上的 `cluster` 也会触发 `'listening'` 事件。

事件句柄使用两个参数来执行，其中 `worker` 包含了工作进程对象，`address` 包含了以下的连接属性：`address`、`port` 和 `addressType`。
当工作进程同时监听多个地址时，这些参数非常有用。

```js
cluster.on('listening', (worker, address) => {
  console.log(
    `工作进程已连接到 ${address.address}:${address.port}`);
});
```

`addressType` 可选值包括:

* `4` (TCPv4)
* `6` (TCPv6)
* `-1` (Unix 域 socket)
* `'udp4'` or `'udp6'` (UDP v4 或 v6)

