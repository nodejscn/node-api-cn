<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {net.Server|net.Socket}
* `options` {Object}
* `callback` {Function}
* 返回: {boolean}

如果 Node.js 进程是通过 IPC 通道衍生的，则 `process.send()` 方法可以用来给父进程发送消息。
接收到的消息被视为父进程的 [`ChildProcess`][] 对象上的一个 [`'message'`][] 事件。

如果 Node.js 进程不是通过 IPC 通道衍生的，则 `process.send()` 将会是 `undefined`。

消息传递时，以格式序列化和解析，结果消息与发送时未必完全一样。

