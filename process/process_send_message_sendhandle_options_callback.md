<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {net.Server|net.Socket}
* `options` {Object} 用于参数化某些类型的句柄的发送。`options` 支持以下属性：
  * `keepOpen` {boolean} 当传递 `net.Socket` 实例时可以使用的值。当为 `true` 时，套接字在发送的过程中保持打开状态。**默认值:** `false`。
* `callback` {Function}
* 返回: {boolean}

如果 Node.js 是使用 IPC 通道衍生的，则可以使用 `process.send()` 方法将消息发送到父进程。
消息将会作为父进程的 [`ChildProcess`] 对象上的 [`'message'`] 事件被接收。

如果 Node.js 不是通过 IPC 通道衍生的，则 `process.send()` 将会是 `undefined`。

消息会进行序列化和解析。
生成的消息可能与最初发送的消息不同。

