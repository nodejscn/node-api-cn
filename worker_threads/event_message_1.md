<!-- YAML
added: v10.5.0
-->

* `value` {any} The transmitted value

The `'message'` event is emitted when the worker thread has invoked
[`require('worker_threads').parentPort.postMessage()`][].
See the [`port.on('message')`][] event for more details.

