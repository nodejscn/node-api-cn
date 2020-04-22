<!-- YAML
added: v13.9.0
-->

* Returns: {Promise} A promise for a Readable Stream containing
  a V8 heap snapshot

Returns a readable stream for a V8 snapshot of the current state of the Worker.
See [`v8.getHeapSnapshot()`][] for more details.

If the Worker thread is no longer running, which may occur before the
[`'exit'` event][] is emitted, the returned `Promise` will be rejected
immediately with an [`ERR_WORKER_NOT_RUNNING`][] error.

