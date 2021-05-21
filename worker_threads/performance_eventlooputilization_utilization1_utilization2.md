<!-- YAML
added:
  - v15.1.0
  - v12.22.0
-->

* `utilization1` {Object} The result of a previous call to
    `eventLoopUtilization()`.
* `utilization2` {Object} The result of a previous call to
    `eventLoopUtilization()` prior to `utilization1`.
* Returns {Object}
  * `idle` {number}
  * `active` {number}
  * `utilization` {number}

The same call as [`perf_hooks` `eventLoopUtilization()`][], except the values
of the worker instance are returned.

One difference is that, unlike the main thread, bootstrapping within a worker
is done within the event loop. So the event loop utilization is
immediately available once the worker's script begins execution.

An `idle` time that does not increase does not indicate that the worker is
stuck in bootstrap. The following examples shows how the worker's entire
lifetime never accumulates any `idle` time, but is still be able to process
messages.

```js
const { Worker, isMainThread, parentPort } = require('worker_threads');

if (isMainThread) {
  const worker = new Worker(__filename);
  setInterval(() => {
    worker.postMessage('hi');
    console.log(worker.performance.eventLoopUtilization());
  }, 100).unref();
  return;
}

parentPort.on('message', () => console.log('msg')).unref();
(function r(n) {
  if (--n < 0) return;
  const t = Date.now();
  while (Date.now() - t < 300);
  setImmediate(r, n);
})(10);
```

The event loop utilization of a worker is available only after the [`'online'`
event][] emitted, and if called before this, or after the [`'exit'`
event][], then all properties have the value of `0`.

