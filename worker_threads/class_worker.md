<!-- YAML
added: v10.5.0
-->

* 继承自: {EventEmitter}

`Worker` 类代表一个独立的 JavaScript 执行线程。
大多数 Node.js API 都在其中可用。

工作线程环境中的显着差异是：

* 父线程可以重定向 [`process.stdin`]、[`process.stdout`] 和 [`process.stderr`]。
* [`require('worker_threads').isMainThread`] 属性被设置为 `false`。
* [`require('worker_threads').parentPort`] 消息端口可用。
* [`process.exit()`] 不会停止整个程序，仅停止单个线程，且 [`process.abort()`] 不可用。
* [`process.chdir()`] 和设置群组或用户标识的 `process` 方法不可用。
* [`process.env`] 是父线程的环境变量的副本，除非另外指定。
  对一个副本的更改将会在其他线程中不可见，并且对原生插件也不可见（除非 [`worker.SHARE_ENV`] 作为 `env` 选项传给 [`Worker`] 的构造函数）。
* [`process.title`] 无法被修改。
* 信号将不会通过 [`process.on('...')`][Signals events] 传递。
* 调用 [`worker.terminate()`] 可能会随时停止执行。
* 无法访问父进程的 IPC 通道。
* 不支持 [`trace_events`] 模块。
* 如果原生插件满足[特定条件][Addons worker support]，则只能从多个线程中加载它们。

可以在其他 `Worker` 实例中创建 `Worker` 实例。

与 [Web 工作线程][Web Workers]和 [`cluster` 模块][`cluster` module]一样，可以通过线程间的消息传递来实现双向通信。 
在内部，一个 `Worker` 具有一对内置的 [`MessagePort`]，在创建该 `Worker` 时它们已经相互关联。 
虽然父端的 `MessagePort` 对象没有直接公开，但其功能是通过父线程的 `Worker` 对象上的 [`worker.postMessage()`] 和 [`worker.on('message')`] 事件公开的。

要创建自定义的消息传递通道（建议使用默认的全局通道，因为这样可以促进关联点的分离），用户可以在任一线程上创建一个 `MessageChannel` 对象，并将该 `MessageChannel` 上的 `MessagePort` 中的一个通过预先存在的通道传给另一个线程，例如全局的通道。

有关如何传递消息以及可以通过线程屏障成功地传输哪类 JavaScript 值的更多信息，请参阅 [`port.postMessage()`]。

```js
const assert = require('assert');
const {
  Worker, MessageChannel, MessagePort, isMainThread, parentPort
} = require('worker_threads');
if (isMainThread) {
  const worker = new Worker(__filename);
  const subChannel = new MessageChannel();
  worker.postMessage({ hereIsYourPort: subChannel.port1 }, [subChannel.port1]);
  subChannel.port2.on('message', (value) => {
    console.log('接收到:', value);
  });
} else {
  parentPort.once('message', (value) => {
    assert(value.hereIsYourPort instanceof MessagePort);
    value.hereIsYourPort.postMessage('工作线程正在发送此消息');
    value.hereIsYourPort.close();
  });
}
```

