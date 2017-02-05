<!-- YAML
added: v0.3.4
-->

HTTP Agent 用于池化在 HTTP 客户端请求中使用的 socket。

HTTP Agent 也默认客户端请求使用 `Connection:keep-alive`。
如果没有挂起的 HTTP 请求正在等待 socket 变成空闲的，则 socket 会被关闭。
这意味着，当在负载状态下但仍不要求开发者使用 KeepAlive 手动关闭 HTTP 客户端时，Node.js 池有 keep-alive 的好处。

如果选择使用 HTTP 的 KeepAlive，可以创建一个将标志设置为 `true` 的 Agent 对象（详见[构造器选项]）。
那么，该 Agent 会保留没用过的 socket 在池中用于后续的使用。
它们会被显式地标记，以便不用保持 Node.js 进程运行。
当然，当它们不再被使用时，应该显式地 [`destroy()`] KeepAlive 代理，以便 Socket 会被关闭。

当 socket 触发一个 `'close'` 事件或一个特殊的 `'agentRemove'` 事件时，socket 会从代理池中被移除。
这意味着，如果打算使一个 HTTP 请求保持长时间打开且不想让它留在池中，则可以如下操作：

```js
http.get(options, (res) => {
  // 处理事情
}).on('socket', (socket) => {
  socket.emit('agentRemove');
});
```

或者，可以选择使用 `agent:false` 完全地退出池：

```js
http.get({
  hostname: 'localhost',
  port: 80,
  path: '/',
  agent: false  // 创建一个新的代理，只用于本次请求
}, (res) => {
  // 对响应进行处理
});
```

