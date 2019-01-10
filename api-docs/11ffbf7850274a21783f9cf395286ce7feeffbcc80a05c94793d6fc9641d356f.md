<!-- YAML
added: v10.5.0
-->

The `Worker` class represents an independent JavaScript execution thread.
Most Node.js APIs are available inside of it.

Notable differences inside a Worker environment are:

- The [`process.stdin`][], [`process.stdout`][] and [`process.stderr`][]
  may be redirected by the parent thread.
- The [`require('worker_threads').isMainThread`][] property is set to `false`.
- The [`require('worker_threads').parentPort`][] message port is available,
- [`process.exit()`][] does not stop the whole program, just the single thread,
  and [`process.abort()`][] is not available.
- [`process.chdir()`][] and `process` methods that set group or user ids
  are not available.
- [`process.env`][] is a read-only reference to the environment variables.
- [`process.title`][] cannot be modified.
- Signals will not be delivered through [`process.on('...')`][Signals events].
- Execution may stop at any point as a result of [`worker.terminate()`][]
  being invoked.
- IPC channels from parent processes are not accessible.

Currently, the following differences also exist until they are addressed:

- The [`inspector`][] module is not available yet.
- Native addons are not supported yet.

Creating `Worker` instances inside of other `Worker`s is possible.

Like [Web Workers][] and the [`cluster` module][], two-way communication can be
achieved through inter-thread message passing. Internally, a `Worker` has a
built-in pair of [`MessagePort`][]s that are already associated with each other
when the `Worker` is created. While the `MessagePort` object on the parent side
is not directly exposed, its functionalities are exposed through
[`worker.postMessage()`][] and the [`worker.on('message')`][] event
on the `Worker` object for the parent thread.

To create custom messaging channels (which is encouraged over using the default
global channel because it facilitates separation of concerns), users can create
a `MessageChannel` object on either thread and pass one of the
`MessagePort`s on that `MessageChannel` to the other thread through a
pre-existing channel, such as the global one.

See [`port.postMessage()`][] for more information on how messages are passed,
and what kind of JavaScript values can be successfully transported through
the thread barrier.

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
    console.log('received:', value);
  });
} else {
  parentPort.once('message', (value) => {
    assert(value.hereIsYourPort instanceof MessagePort);
    value.hereIsYourPort.postMessage('the worker is sending this');
    value.hereIsYourPort.close();
  });
}
```

