<!-- YAML
added: v10.5.0
-->

* {null|MessagePort}

如果当前线程为[`Worker`][]工作线程, 该[`MessagePort`][]端口作用于与主线交换信息。通过该端口`parentPort.postMessage()`发送的消息在主线程中将可以通过`worker.on('message')`接收。主线程中通过`worker.postMessage()`发送的消息将可以在工作线程中通过`parentPort.on('message')`接收。

```js
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.once('message', (message) => {
    console.log(message);  // Prints 'Hello, world!'.
  });
  worker.postMessage('Hello, world!');
} else {
  // When a message from the parent thread is received, send it back:
  parentPort.once('message', (message) => {
    parentPort.postMessage(message);
  });
}
```

