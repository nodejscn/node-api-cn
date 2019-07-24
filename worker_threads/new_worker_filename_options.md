
* `filename` {string} The path to the Worker’s main script. Must be
  either an absolute path or a relative path (i.e. relative to the
  current working directory) starting with `./` or `../`.
  If `options.eval` is `true`, this is a string containing JavaScript code
  rather than a path.
* `options` {Object}
  * `env` {Object} If set, specifies the initial value of `process.env` inside
    the Worker thread. As a special value, [`worker.SHARE_ENV`][] may be used
    to specify that the parent thread and the child thread should share their
    environment variables; in that case, changes to one thread’s `process.env`
    object will affect the other thread as well. **Default:** `process.env`.
  * `eval` {boolean} If `true`, interpret the first argument to the constructor
    as a script that is executed once the worker is online.
  * `execArgv` {string[]} List of node CLI options passed to the worker.
    V8 options (such as `--max-old-space-size`) and options that affect the
    process (such as `--title`) are not supported. If set, this will be provided
    as [`process.execArgv`][] inside the worker. By default, options will be
    inherited from the parent thread.
  * `stdin` {boolean} If this is set to `true`, then `worker.stdin` will
    provide a writable stream whose contents will appear as `process.stdin`
    inside the Worker. By default, no data is provided.
  * `stdout` {boolean} If this is set to `true`, then `worker.stdout` will
    not automatically be piped through to `process.stdout` in the parent.
  * `stderr` {boolean} If this is set to `true`, then `worker.stderr` will
    not automatically be piped through to `process.stderr` in the parent.
  * `workerData` {any} Any JavaScript value that will be cloned and made
    available as [`require('worker_threads').workerData`][]. The cloning will
    occur as described in the [HTML structured clone algorithm][], and an error
    will be thrown if the object cannot be cloned (e.g. because it contains
    `function`s).

