<!-- YAML
added: v10.5.0
-->

* {null|MessagePort}

If this thread was spawned as a [`Worker`][], this will be a [`MessagePort`][]
allowing communication with the parent thread. Messages sent using
`parentPort.postMessage()` will be available in the parent thread
using `worker.on('message')`, and messages sent from the parent thread
using `worker.postMessage()` will be available in this thread using
`parentPort.on('message')`.

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

