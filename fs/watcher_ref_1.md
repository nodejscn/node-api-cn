<!-- YAML
added: v14.3.0
-->

* Returns: {fs.StatWatcher}

When called, requests that the Node.js event loop *not* exit so long as the
`StatWatcher` is active. Calling `watcher.ref()` multiple times will have
no effect.

By default, all `StatWatcher` objects are "ref'ed", making it normally
unnecessary to call `watcher.ref()` unless `watcher.unref()` had been
called previously.

