<!-- YAML
added: v16.0.0
-->

* `settings` {Object} See [`cluster.settings`][].

`setupPrimary` is used to change the default 'fork' behavior. Once called,
the settings will be present in `cluster.settings`.

Any settings changes only affect future calls to [`.fork()`][] and have no
effect on workers that are already running.

The only attribute of a worker that cannot be set via `.setupPrimary()` is
the `env` passed to [`.fork()`][].

The defaults above apply to the first call only; the defaults for later
calls are the current values at the time of `cluster.setupPrimary()` is called.

```js
const cluster = require('cluster');
cluster.setupPrimary({
  exec: 'worker.js',
  args: ['--use', 'https'],
  silent: true
});
cluster.fork(); // https worker
cluster.setupPrimary({
  exec: 'worker.js',
  args: ['--use', 'http']
});
cluster.fork(); // http worker
```

This can only be called from the primary process.

