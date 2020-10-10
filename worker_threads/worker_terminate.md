<!-- YAML
added: v10.5.0
changes:
  - version: v12.5.0
    pr-url: https://github.com/nodejs/node/pull/28021
    description: This function now returns a Promise.
                 Passing a callback is deprecated, and was useless up to this
                 version, as the Worker was actually terminated synchronously.
                 Terminating is now a fully asynchronous operation.
-->

* Returns: {Promise}

Stop all JavaScript execution in the worker thread as soon as possible.
Returns a Promise for the exit code that is fulfilled when the
[`'exit'` event][] is emitted.

