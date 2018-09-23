
<!--introduced_in=v10.5.0-->

> Stability: 1 - Experimental

The `worker` module provides a way to create multiple environments running
on independent threads, and to create message channels between them. It
can be accessed using the `--experimental-worker` flag and:

```js
const worker = require('worker_threads');
```

Workers are useful for performing CPU-intensive JavaScript operations; do not
use them for I/O, since Node.js’s built-in mechanisms for performing operations
asynchronously already treat it more efficiently than Worker threads can.

Workers, unlike child processes or when using the `cluster` module, can also
share memory efficiently by transferring `ArrayBuffer` instances or sharing
`SharedArrayBuffer` instances between them.

```js
const {
  Worker, isMainThread, parentPort, workerData
} = require('worker_threads');

if (isMainThread) {
  module.exports = async function parseJSAsync(script) {
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

Note that this example spawns a Worker thread for each `parse` call.
In practice, it is strongly recommended to use a pool of Workers for these
kinds of tasks, since the overhead of creating Workers would likely exceed the
benefit of handing the work off to it.

