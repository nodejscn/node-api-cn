<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11985
    description: The `msg` parameter can be an Uint8Array now.
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

* `msg` {Buffer|Uint8Array|string|array} 要发送的消息
* `offset` {number} 整数。可选。指定消息的开头在 buffer 中的偏移量。
* `length` {number} 整数。可选。消息的字节数。
* `port` {number} 整数。目标端口。
* `address` {string} 目标主机名或 IP 地址。可选的。
* `callback` {Function} 当消息被发送时会被调用。可选的。

在 socket 上发送一个数据包。目标`port`和`address`须被指定。

`msg`参数包含了要发送的消息。根据消息的类型可以有不同的做法。如果`msg`是一个`Buffer` 或 `Uint8Array`，则`offset`和`length`指定了消息在`Buffer`中对应的偏移量和字节数。如果`msg`是一个`String`，那么它会被自动地按照`utf8`编码转换为`Buffer`。对于包含了多字节字符的消息，`offset`和`length`会根据对应的[byte length][]进行计算，而不是根据字符的位置。如果`msg`是一个数组，那么`offset`和`length`必须都不能被指定。

`address`参数是一个字符串。若`address`的值是一个主机名，则 DNS 会被用来解析主机的地址。若`address`未提供或是非真值，则`'127.0.0.1'`（用于 `udp4` socket）或`'::1'`（用于 `udp6` socket）会被使用。

若在之前 socket 未通过调用`bind`方法进行绑定，socket 将会被一个随机的端口号赋值并绑定到“所有接口”的地址上（对于`udp4` socket 是`'0.0.0.0'`，对于`udp6` socket 是`'::0'`）。

可以指定一个可选的`callback`方法来汇报 DNS 错误或判断可以安全地重用`buf`对象的时机。注意，在 Node.js 事件循环中，DNS 查询会对发送造成至少 1 tick 的延迟。

确定数据包被发送的唯一方式就是指定`callback`。若在`callback`被指定的情况下有错误发生，该错误会作为`callback`的第一个参数。若`callback`未被指定，该错误会以`'error'`事件的方式投射到`socket`对象上。

偏移量和长度是可选的，但如其中一个被指定则另一个也必须被指定。另外，他们只在第一个参数是`Buffer` 或 `Uint8Array` 的情况下才能被使用。

一个发送 UDP 包到`localhost`上的某个随机端口的例子：

```js
const dgram = require('dgram');
const message = Buffer.from('Some bytes');
const client = dgram.createSocket('udp4');
client.send(message, 41234, 'localhost', (err) => {
  client.close();
});
```

一个发送包含多个 buffer 的 UDP 包到 `127.0.0.1` 上的某个随机端口的例子：

```js
const dgram = require('dgram');
const buf1 = Buffer.from('Some ');
const buf2 = Buffer.from('bytes');
const client = dgram.createSocket('udp4');
client.send([buf1, buf2], 41234, (err) => {
  client.close();
});
```

发送多个 buffer 的速度取决于应用和操作系统。
It is important to run benchmarks to
determine the optimal strategy on a case-by-case basis. Generally speaking,
however, sending multiple buffers is faster.

**关于 UDP 包大小的注意事项**

`IPv4/v6`数据包的最大尺寸取决于`MTU`(_Maximum Transmission Unit_, 最大传输单元)与`Payload Length`字段大小。

- `Payload Length`字段有`16 位`宽，指一个超过 64K 的_包含_ IP 头部和数据的负载 (65,507 字节 = 65,535 − 8 字节 UDP 头 − 20 字节 IP 头部)；通常对于环回地址来说是这样，但这个长度的数据包对于大多数的主机和网络来说不切实际。

- `MTU`指的是数据链路层为数据包提供的最大大小。对于任意链路，`IPv4`所托管的`MTU`最小为`68`个字节，推荐为`576`（典型地，作为拨号上网应用的推荐值），无论它们是完整地还是分块地抵达。

  对于`IPv6`，`MTU`的最小值是`1280`个字节，然而，受托管的最小的碎片重组缓冲大小为`1500`个字节。现今大多数的数据链路层技术（如以太网），都有`1500`的`MTU`最小值，因而`68`个字节显得非常小。

要提前知道数据包可能经过的每个链路的 MTU 是不可能的。发送大于接受者`MTU`大小的数据包将不会起作用，因为数据包会被静默地丢失，而不会通知发送者该包未抵达目的地。

