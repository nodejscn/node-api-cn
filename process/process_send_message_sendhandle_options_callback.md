<!-- YAML
added: v0.5.9
-->

* `message` {Object}
* `sendHandle` {net.Server|net.Socket}
* `options` {Object}
* `callback` {Function}
* Returns: {boolean}

如果Node.js进程是通过进程间通信产生的，那么，process.send()方法可以用来给父进程发送消息。
接收到的消息被视为父进程的[`ChildProcess`][]对象上的一个[`'message'`][]事件。

如果Node.js进程不是通过进程间通信产生的， `process.send()` 会是`undefined`。

*注意*: 消息传递时，以格式序列化和解析，结果消息与发送时未必完全一样。
