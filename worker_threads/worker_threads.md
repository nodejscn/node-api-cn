
<!--introduced_in=v10.5.0-->

> 稳定性: 2 - 稳定

`worker_threads` 模块允许使用并行地执行 JavaScript 的线程。 
要访问它：

```js
const worker = require('worker_threads');
```

工作线程对于执行 CPU 密集型的 JavaScript 操作非常有用。 
它们在 I/O 密集型的工作中用途不大。 
Node.js 的内置的异步 I/O 操作比工作线程效率更高。

与 `child_process` 或 `cluster` 不同，`worker_threads` 可以共享内存。 
它们通过传输 `ArrayBuffer` 实例或共享 `SharedArrayBuffer` 实例来实现。

```js
const {
  Worker, isMainThread, parentPort, workerData
} = require('worker_threads');

if (isMainThread) {
  module.exports = function parseJSAsync(script) {
    return new Promise((resolve, reject) => {
      const worker = new Worker(__filename, {
        workerData: script
      });
      worker.on('message', resolve);
      worker.on('error', reject);
      worker.on('exit', (code) => {
        if (code !== 0)
          reject(new Error(`工作线程使用退出码 ${code} 停止`));
      });
    });
  };
} else {
  const { parse } = require('一些 js 解析库');
  const script = workerData;
  parentPort.postMessage(parse(script));
}
```

上面的示例为每个 `parse()` 调用衍生一个工作线程。 
在实际的实践中，应使用工作线程池代替这些任务。 
否则，创建工作线程的开销可能会超出其收益。

当实现工作线程池时，可使用 [`AsyncResource`] API 来通知诊断的工具（例如为了提供异步的堆栈跟踪）有关任务及其结果之间的相关性。
有关示例的实现，请参见 `async_hooks` 文档中的[“为 `Worker` 线程池使用 `AsyncResource`”][async-resource-worker-pool]。

默认情况下，工作线程继承非特定于进程的选项。 
请参见[工作线程的构造函数选项][`Worker constructor options`]，以了解如何自定义工作线程的选项，特别是 `argv` 和 `execArgv` 选项。

