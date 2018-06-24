
* `filename` {string} The absolute path to the Worker’s main script.
  If `options.eval` is true, this is a string containing JavaScript code rather
  than a path.
* `options` {Object}
  * `eval` {boolean} If true, interpret the first argument to the constructor
    as a script that is executed once the worker is online.
  * `workerData` {any} Any JavaScript value that will be cloned and made
    available as [`require('worker_threads').workerData`][]. The cloning will
    occur as described in the [HTML structured clone algorithm][], and an error
    will be thrown if the object cannot be cloned (e.g. because it contains
    `function`s).
  * stdin {boolean} If this is set to `true`, then `worker.stdin` will
    provide a writable stream whose contents will appear as `process.stdin`
    inside the Worker. By default, no data is provided.
  * stdout {boolean} If this is set to `true`, then `worker.stdout` will
    not automatically be piped through to `process.stdout` in the parent.
  * stderr {boolean} If this is set to `true`, then `worker.stderr` will
    not automatically be piped through to `process.stderr` in the parent.

