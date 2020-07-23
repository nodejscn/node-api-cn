<!-- YAML
added: v0.6.9
-->

* `multicastAddress` {string}
* `multicastInterface` {string}

通知内核将 `multicastAddress` 和 `multicastInterface` 提供的多路传送集合通过 `IP_ADD_MEMBERSHIP` 这个 socket 选项结合起来。
若 `multicastInterface` 参数未指定，则操作系统将会选择一个接口并向其添加成员。
要为所有可用的接口添加成员，可以在每个接口上调用一次 `addMembership` 方法。

When called on an unbound socket, this method will implicitly bind to a random
port, listening on all interfaces.

当多个 `cluster` 工作进程之间共享 UDP socket 时，则 `socket.addMembership()` 函数必须只能被调用一次，否则将会发生 `EADDRINUSE` 错误：

```js
const cluster = require('cluster');
const dgram = require('dgram');
if (cluster.isMaster) {
  cluster.fork(); // 可工作。
  cluster.fork(); // 失败并抛出 EADDRINUSE。
} else {
  const s = dgram.createSocket('udp4');
  s.bind(1234, () => {
    s.addMembership('224.0.0.114');
  });
}
```

