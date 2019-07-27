<!-- YAML
added: v0.11.14
-->

* `options` {Object} 必要的。包含以下属性：
  * `port` {integer}
  * `address` {string}
  * `exclusive` {boolean}
  * `fd` {integer}
* `callback` {Function}

对于 UDP socket，该方法会令 `dgram.Socket` 在指定的 `port` 和可选的 `address` 上监听数据包信息。
若 `port` 未指定或为 `0`，操作系统会尝试绑定一个随机的端口。
若 `address` 未指定，操作系统会尝试在所有地址上监听。
绑定完成时会触发一个 `'listening'` 事件，并会调用 `callback` 方法。

`options` 对象可能包含 `fd` 属性。 
当设置大于 `0` 的 `fd` 时，它将会使用给定的文件描述符封装一个现有的 socket。 
在这种情况下，`port` 和 `address` 的属性将会忽略。

同时监听 `'listening'` 事件和在 `socket.bind()` 方法中传入 `callback` 参数并不会带来坏处，但也不是很有用。

在配合 [`cluster`] 模块使用 `dgram.Socket` 对象时，`options` 对象可能包含一个附加的 `exclusive` 属性。
当 `exclusive` 被设为 `false`（默认值）时，集群工作进程会使用相同的 socket 句柄来共享连接处理作业。
当 `exclusive` 被设为 `true` 时，该句柄将不会被共享，而尝试共享端口则会造成错误。

一个绑定的数据报 socket 会使 Node.js 进程持续运行以接受数据报消息。

如果绑定失败，一个 `'error'` 事件会产生。在极少数情况下（例如尝试绑定一个已经关闭的 socket），一个 [`Error`] 可能抛出。

一个不共享端口的 socket 的例子如下文所示。


```js
socket.bind({
  address: 'localhost',
  port: 8000,
  exclusive: true
});
```

