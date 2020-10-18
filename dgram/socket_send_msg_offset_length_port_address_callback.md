<!-- YAML
added: v0.1.99
changes:
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/22413
    description: The `msg` parameter can now be any `TypedArray` or `DataView`.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26871
    description: Added support for sending data on connected sockets.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11985
    description: The `msg` parameter can be an `Uint8Array` now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10473
    description: The `address` parameter is always optional now.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5929
    description: On success, `callback` will now be called with an `error`
                 argument of `null` rather than `0`.
  - version: v5.7.0
    pr-url: https://github.com/nodejs/node/pull/4374
    description: The `msg` parameter can be an array now. Also, the `offset`
                 and `length` parameters are optional now.
-->

* `msg` {Buffer|TypedArray|DataView|string|Array} 要发送的消息。
* `offset` {integer} 指定消息的开头在 buffer 中的偏移量。
* `length` {integer} 消息的字节数。
* `port` {integer} 目标端口。
* `address` {string} 目标主机名或 IP 地址。
* `callback` {Function} 当消息被发送时会被调用。

在 socket 上广播一个数据包。
对于无连接的 socket，必须指定目标的 `port` 和 `address`。 
对于连接的 socket，则将会使用其关联的远程端点，因此不能设置 `port` 和 `address` 参数。

`msg` 参数包含了要发送的消息。
根据消息的类型可以有不同的做法。
如果 `msg` 是一个 `Buffer`、`TypedArray` 或 `DataView`，则 `offset` 和 `length` 指定了消息在 `Buffer` 中对应的偏移量和字节数。
如果 `msg` 是一个` String`，那么它会被自动地按照 `'utf8'` 编码转换为 `Buffer`。
对于包含了多字节字符的消息，`offset` 和 `length` 会根据对应的[字节长度][byte length]进行计算，而不是根据字符的位置。
如果 `msg` 是一个数组，那么 `offset` 和 `length` 必须都不能被指定。

`address` 参数是一个字符串。
若 `address` 的值是一个主机名，则 DNS 会被用来解析主机的地址。
若 `address` 未提供或是非真值，则 `'127.0.0.1'`（用于 `udp4` socket）或 `'::1'`（用于 `udp6` socket）会被使用。

若在之前 socket 未通过调用 `bind` 方法进行绑定，socket 将会被一个随机的端口号赋值并绑定到“所有接口”的地址上（对于 `udp4` socket 是 `'0.0.0.0'`，对于 `udp6` socket 是 `'::0'`）。

可以指定一个可选的 `callback` 方法来汇报 DNS 错误或判断可以安全地重用 `buf` 对象的时机。
在 Node.js 事件循环中，DNS 查询会对发送造成至少一个时间点的延迟。

确定数据包被发送的唯一方式就是指定 `callback`。
若在 `callback` 被指定的情况下有错误发生，该错误会作为 `callback` 的第一个参数。
若 `callback` 未被指定，该错误会以 `'error'` 事件的方式投射到 `socket` 对象上。

偏移量和长度是可选的，但如其中一个被指定则另一个也必须被指定。
另外，它们只在第一个参数是 `Buffer`、`TypedArray` 或 `DataView` 的情况下才能被使用。

This method throws [`ERR_SOCKET_BAD_PORT`][] if called on an unbound socket.

示例，发送 UDP 包到 `localhost` 上的某个端口：

```js
const dgram = require('dgram');
const message = Buffer.from('一些字节');
const client = dgram.createSocket('udp4');
client.send(message, 41234, 'localhost', (err) => {
  client.close();
});
```

示例，发送包含多个 buffer 的 UDP 包到 `127.0.0.1` 上的某个端口：

```js
const dgram = require('dgram');
const buf1 = Buffer.from('一些 ');
const buf2 = Buffer.from('字节');
const client = dgram.createSocket('udp4');
client.send([buf1, buf2], 41234, (err) => {
  client.close();
});
```

发送多个 buffer 的速度取决于应用和操作系统。
逐案运行基准来确定最佳策略。
但是一般来说，发送多个 buffer 速度更快。

示例，使用已连接的 socket 发送 UDP 包到 `localhost` 上的某个端口：

```js
const dgram = require('dgram');
const message = Buffer.from('一些字节');
const client = dgram.createSocket('udp4');
client.connect(41234, 'localhost', (err) => {
  client.send(message, (err) => {
    client.close();
  });
});
```

