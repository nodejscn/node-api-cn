<!-- YAML
added: v0.5.8
-->

Objects returned from [`fs.watch()`][] are of this type.

The `listener` callback provided to `fs.watch()` receives the returned FSWatcher's
`change` events.

The object itself emits these events:

