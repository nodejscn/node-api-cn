
<!--introduced_in=v10.5.0-->

> Stability: 2 - Stable

The `worker_threads` module enables the use of threads that execute JavaScript
in parallel. To access it:

```js
const worker = require('worker_threads');
```

Workers (threads) are useful for performing CPU-intensive JavaScript operations.
They will not help much with I/O-intensive work. Node.js’s built-in asynchronous
I/O operations are more efficient than Workers can be.

Unlike `child_process` or `cluster`, `worker_threads` can share memory. They do
so by transferring `ArrayBuffer` instances or sharing `SharedArrayBuffer`
instances.

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
          reject(new Error(`Worker stopped with exit code ${code}`));
      });
    });
  };
} else {
  const { parse } = require('some-js-parsing-library');
  const script = workerData;
  parentPort.postMessage(parse(script));
}
```

The above example spawns a Worker thread for each `parse()` call. In actual
practice, use a pool of Workers instead for these kinds of tasks. Otherwise, the
overhead of creating Workers would likely exceed their benefit.

When implementing a worker pool, use the [`AsyncResource`][] API to inform
diagnostic tools (e.g. in order to provide asynchronous stack traces) about the
correlation between tasks and their outcomes.

