<!-- YAML
added: v14.3.0
-->

* Returns: {fs.StatWatcher}

When called, the active `StatWatcher` object will not require the Node.js
event loop to remain active. If there is no other activity keeping the
event loop running, the process may exit before the `StatWatcher` object's
callback is invoked. Calling `watcher.unref()` multiple times will have
no effect.

