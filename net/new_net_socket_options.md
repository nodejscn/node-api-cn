<!-- YAML
added: v0.3.4
-->


创建一个 socket 对象。

* `options` {Object} 可用选项有：
  * `fd`: {number} 如果指定了该参数，则使用一个给定的文件描述符包装一个已存在的 socket，否则将创建一个新的 socket。
  * `allowHalfOpen` {boolean} 指示是否允许半打开的 TCP 连接。详情查看 [`net.createServer()`][] 和 [`'end'`][] 事件。默认是 `false`。
  * `readable` {boolean} 当传递了 `fd` 时允许读取 socket，否则忽略。默认 `false`。
  * `writable` {boolean} 当传递了 `fd` 时允许写入 socket，否则忽略。默认 `false`。
* Returns: {net.Socket}

新创建的 socket 可以是 TCP socket 也可以是 [IPC][] 端点流，取决于它连接 [`connect()`][`socket.connect()`] 到什么。
