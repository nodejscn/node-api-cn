<!-- YAML
added: v0.1.90
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/25436
    description: Added `onread` option.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6021
    description: The `hints` option defaults to `0` in all cases now.
                 Previously, in the absence of the `family` option it would
                 default to `dns.ADDRCONFIG | dns.V4MAPPED`.
  - version: v5.11.0
    pr-url: https://github.com/nodejs/node/pull/6000
    description: The `hints` option is supported now.
-->

* `options` {Object}
* `connectListener` {Function} [`socket.connect()`] 方法的通用参数。将会作为 [`'connect'`] 事件的监听器被添加一次。
* 返回: {net.Socket} 套接字自身。

在给定的套接字上启动连接。
通常不需要此方法，应该使用 [`net.createConnection()`] 来创建和打开套接字。
仅在实现自定义的套接字时才使用此方法。

对于 TCP 连接，可用的 `options` 有：

* `port` {number} 必须。套接字要连接的端口。
* `host` {string} 套接字要连接的主机。**默认值:** `'localhost'`。
* `localAddress` {string} 套接字要连接的本地地址。
* `localPort` {number} 套接字要连接的本地端口。
* `family` {number} IP 栈的版本。必须为 `4`、`6` 或 `0`。`0` 值表示允许 IPv4 和 IPv6 地址。**默认值:** `0`。
* `hints` {number} 可选的 [`dns.lookup()` 提示][`dns.lookup()` hints]。
* `lookup` {Function} 自定义的查找函数。**默认值:** [`dns.lookup()`]。

对于 [IPC] 连接，可用的 `options` 有：

* `path` {string} 必须。客户端要连接的路径。参阅[识别 IPC 连接的路径][Identifying paths for IPC connections]。如果提供了，则忽略上面的 TCP 特定的选项。

对于这两种类型，可用 `options` 包括：

* `onread` {Object} - 如果指定，则传入的数据会存储在单个 `buffer` 中，并在数据到达套接字时传给提供的 `callback`。 
   这将会导致流式的功能不会提供任何数据，但 `'error'`、`'end'` 和 `'close'` 等事件仍将会被正常触发，且 `pause()` 和 `resume()` 等方法也将会按预期运行。
  * `buffer` {Buffer|Uint8Array|Function} - 用于存储传入数据的可复用的内存块、或返回此类数据的函数。
  * `callback` {Function} 为每个传入的数据块调用此函数。有两个参数传给它：写入 `buffer` 的字节数和对 `buffer` 的引用。从此函数返回 `false` 可以隐式地 `pause()` 套接字。该函数将会在全局的上下文中执行。

以下是使用 `onread` 选项的客户端的示例：

```js
const net = require('net');
net.connect({
  port: 80,
  onread: {
    // 为套接字的每次读取复用 4KiB 的 Buffer。
    buffer: Buffer.alloc(4 * 1024),
    callback: function(nread, buf) {
      // 收到的数据在 `buf` 中可用，从 0 到 'nread`。
      console.log(buf.toString('utf8', 0, nread));
    }
  }
});
```

