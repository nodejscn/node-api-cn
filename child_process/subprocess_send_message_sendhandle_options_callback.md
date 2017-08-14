<!-- YAML
added: v0.5.9
changes:
  - version: v5.8.0
    pr-url: https://github.com/nodejs/node/pull/5283
    description: The `options` parameter, and the `keepOpen` option
                 in particular, is supported now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3516
    description: This method returns a boolean for flow control now.
  - version: v4.0.0
    pr-url: https://github.com/nodejs/node/pull/2620
    description: The `callback` parameter is supported now.
-->

* `message` {Object}
* `sendHandle` {Handle}
* `options` {Object}
* `callback` {Function}
* 返回: {boolean}

当父进程和子进程之间建立了一个 IPC 通道时（例如，使用 [`child_process.fork()`]），`subprocess.send()` 方法可用于发送消息到子进程。
当子进程是一个 Node.js 实例时，消息可以通过 [`process.on('message')`] 事件接收。

例子，父进程脚本如下：

```js
const cp = require('child_process');
const n = cp.fork(`${__dirname}/sub.js`);

n.on('message', (m) => {
  console.log('父进程收到消息：', m);
});

n.send({ hello: 'world' });
```

然后是子进程脚本，`'sub.js'` 可能看上去像这样：

```js
process.on('message', (m) => {
  console.log('子进程收到消息：', m);
});

process.send({ foo: 'bar' });
```

Node.js 中的子进程有一个自己的 [`process.send()`] 方法，允许子进程发送消息回父进程。

当发送一个 `{cmd: 'NODE_foo'}` 消息时，是一个特例。
所有在 `cmd` 属性里包含一个 `NODE_` 前缀的都会被认为是预留给 Node.js 核心代码内部使用的，且不会触发子进程的 [`process.on('message')`] 事件。
而是，这种消息可使用 `process.on('internalMessage')` 事件触发，且被 Node.js 内部消费。
应用程序应避免使用这种消息或监听 `'internalMessage'` 事件。

可选的 `sendHandle` 参数可能被传给 `subprocess.send()`，它用于传入一个 TCP 服务器或 socket 对象给子进程。
子进程会接收对象作为第二个参数，并传给注册在 [`process.on('message')`] 事件上的回调函数。
socket 上接收或缓冲的任何数据不会被发送给子进程。

`options` 参数，如果存在的话，是一个用于处理发送数据参数对象。`options` 支持以下属性：

  * `keepOpen` - 一个 Boolean 值，当传入 `net.Socket` 实例时可用。
    当为 `true` 时，socket 在发送进程中保持打开。
    默认为 `false`。

可选的 `callback` 是一个函数，它在消息发送之后、子进程收到消息之前被调用。
该函数被调用时只有一个参数：成功时是 `null`，失败时是一个 [`Error`] 对象。

如果没有提供 `callback` 函数，且消息没被发送，则一个 `'error'` 事件将被 [`ChildProcess`] 对象触发。
这是有可能发生的，例如当子进程已经退出时。

如果通道已关闭，或当未发送的消息的积压超过阈值使其无法发送更多时，`subprocess.send()` 会返回 `false`。
除此以外，该方法返回 `true`。
`callback` 函数可用于实现流量控制。

