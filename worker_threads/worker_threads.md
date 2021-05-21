
<!--introduced_in=v10.5.0-->

> 稳定性: 2 - 稳定的

<!-- source_link=lib/worker_threads.js -->

`worker_threads` 模块使能够使用并行地执行 JavaScript 的线程。 
要访问它：

```js
const worker = require('worker_threads');
```

工作线程对于执行 CPU 密集型的 JavaScript 操作非常有用。 
它们对于 I/O 密集型的工作帮助不大。 
Node.js 内置的异步 I/O 操作比工作线程效率更高。

不同于 `child_process` 或者 `cluster`，`worker_threads` 可以共享内存。 
它们通过传输 `ArrayBuffer` 实例或者共享 `SharedArrayBuffer` 实例来做到。

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
          reject(new Error(`工作线程被退出码 ${code} 停止`));
      });
    });
  };
} else {
  const { parse } = require('some-js-parsing-library');
  const script = workerData;
  parentPort.postMessage(parse(script));
}
```

上面的示例为每个 `parse()` 调用衍生一个工作线程。 
在实际的实践中，为这类任务使用一个工作线程池。 
否则，创建工作线程的开销可能超出其收益。

当实现一个工作线程池时，使用 [`AsyncResource`] API 来通知诊断的工具（例如为了提供异步的堆栈跟踪）关于任务及其结果之间的相关性。
查看 `async_hooks` 文档中的[“为一个工作线程池使用 `AsyncResource`”][async-resource-worker-pool]获取一个示例实现。

默认情况下，工作线程继承非进程特定的选项。 
查看[工作线程的构造器选项][`Worker constructor options`]了解如何自定义工作线程的选项，特别是 `argv` 和 `execArgv` 选项。

