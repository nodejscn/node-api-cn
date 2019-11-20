<!-- YAML
added: v0.7.1
changes:
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7838
    description: The `stdio` option is supported now.
-->

* `settings` {Object} 详见 [`cluster.settings`]。

`setupMaster` 用于修改默认的 'fork' 行为。
一旦调用，将会按照 `cluster.settings` 进行设置。

所有的设置只对后来的 [`.fork()`] 调用有效，对之前的工作进程无影响。

唯一无法通过 `.setupMaster()` 设置的属性是传给 [`.fork()`] 的 `env` 属性。

上述的默认值只在第一次调用时有效，当后续调用时，将采用 `cluster.setupMaster()` 调用时的当前值。

```js
const cluster = require('cluster');
cluster.setupMaster({
  exec: 'worker.js',
  args: ['--use', 'https'],
  silent: true
});
cluster.fork(); // https 工作进程
cluster.setupMaster({
  exec: 'worker.js',
  args: ['--use', 'http']
});
cluster.fork(); // http 工作进程
```

这只能由主进程调用。

