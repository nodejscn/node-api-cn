<!-- YAML
added: v11.13.0
-->

* `filename` {string} 要保存 V8 堆快照的文件路径。 
  如果未指定，则将会生成具有 `'Heap-${yyyymmdd}-${hhmmss}-${pid}-${thread_id}.heapsnapshot'` 模式的文件名，
  其中 `{pid}` 将会是 Node.js 进程的 PID，`{thread_id}` 将会为 `0`（当从主 Node.js 线程调用 `writeHeapSnapshot()` 时）或工作线程的 id。
* 返回: {string} 保存快照的文件名。

生成当前 V8 堆的快照并将其写入 JSON 文件。 
此文件旨在与 Chrome DevTools 等工具一起使用。 
JSON 模式未记录且特定于V8引擎，并且可能从 V8 的一个版本更改为下一个版本。

堆快照特定于单个 V8 隔离。 
使用[工作线程][Worker Threads]时，从主线程生成的堆快照将不包含有关工作线程的任何信息，反之亦然。

```js
const { writeHeapSnapshot } = require('v8');
const {
  Worker,
  isMainThread,
  parentPort
} = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename);

  worker.once('message', (filename) => {
    console.log(`工作线程的堆转储: ${filename}`);
    // 获取主线程的堆转储。
    console.log(`主线程的堆转储: ${writeHeapSnapshot()}`);
  });

  // 通知工作线程创建一个堆转储。
  worker.postMessage('heapdump');
} else {
  parentPort.once('message', (message) => {
    if (message === 'heapdump') {
      // 为工作线程生成一个堆转储，并返回文件名到父线程。
      parentPort.postMessage(writeHeapSnapshot());
    }
  });
}
```

