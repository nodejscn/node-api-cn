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
* `options` {Object} `options` 参数（如果存在）是一个对象，用于参数化某些类型句柄的发送。`options` 支持以下属性：
  * `keepOpen` {boolean} 传给 `net.Socket` 实例时可以使用的值。当设为 `true` 时，则 socket 在发送过程中会保持打开状态。**默认值:** `false`。
* `callback` {Function}
* 返回: {boolean}

当父进程和子进程之间已建立了一个 IPC 通道时（例如，使用 [`child_process.fork()`]），`subprocess.send()` 方法可用于发送消息到子进程。
当子进程是一个 Node.js 实例时，则消息可以通过 [`'message'`] 事件接收。

消息通过序列化和解析进行传递，接收到消息可能跟最初发送的不完全一样。

例如，在父进程的脚本中：

```js
const cp = require('child_process');
const n = cp.fork(`${__dirname}/sub.js`);

n.on('message', (m) => {
  console.log('父进程收到消息', m);
});

// 使子进程打印: 子进程收到消息 { hello: 'world' }
n.send({ hello: 'world' });
```

子进程的脚本 `'sub.js'` 可能如下：

```js
process.on('message', (m) => {
  console.log('子进程收到消息', m);
});

// 使父进程输出: 父进程收到消息 { foo: 'bar', baz: null }
process.send({ foo: 'bar', baz: NaN });
```

子 Node.js 进程有一个自己的 [`process.send()`] 方法，允许子进程发送消息回父进程。

当发送 `{cmd: 'NODE_foo'}` 消息时有一种特殊情况。
`cmd` 属性中包含 `NODE_` 前缀的消息是预留给 Node.js 内核内部使用的，将不会触发子进程的 [`'message'`] 事件。
相反，这种消息可使用 `'internalMessage'` 事件触发，且会被 Node.js 内部消费。
应用程序应避免使用此类消息或监听 `'internalMessage'` 事件，因为它可能会被更改且不会通知。

可能传给 `subprocess.send()` 的可选的 `sendHandle` 参数用于将 TCP 服务器或 socket 对象传给子进程。
子进程将会接收该对象作为传给在 [`'message'`] 事件上注册的回调函数的第二个参数。
在 socket 中接收和缓冲的任何数据都不会被发送给子进程。

可选的 `callback` 是一个函数，它在消息被发送之后、子进程已收到消息之前被调用。
该函数被调用时只有一个参数：当成功时是 `null`，当失败时是一个 [`Error`] 对象。

如果没有提供 `callback` 函数，且消息无法被发送，则 [`ChildProcess`] 对象将会触发 `'error'` 事件。
这是有可能发生的，例如当子进程已经退出时。

如果通道已关闭、或当未发送的消息的积压超过阈值使其无法发送更多时，`subprocess.send()` 将会返回 `false`。
否则，该方法返回 `true`。
`callback` 函数可用于实现流量控制。

