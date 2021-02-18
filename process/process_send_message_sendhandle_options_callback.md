<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {net.Server|net.Socket}
* `options` {Object} 用于参数化特定类型的句柄的发送。`options` 支持以下属性：
  * `keepOpen` {boolean} 当传递 `net.Socket` 实例时可以使用的值。
    当为 `true` 时，则 socket 在发送的过程中会保持打开。
    **默认值:** `false`。
* `callback` {Function}
* 返回: {boolean}

如果 Node.js 是使用 IPC 通道衍生的，则可以使用 `process.send()` 方法发送消息到父进程。
消息会被接收为父进程的 [`ChildProcess`] 对象上的 [`'message'`] 事件。

如果 Node.js 不是通过 IPC 通道衍生的，则 `process.send` 会是 `undefined`。

消息会进行序列化和解析。
生成的消息可能与最初发送的消息不同。

