<!-- YAML
added: v14.3.0
-->

* Returns: {fs.FSWatcher}

When called, the active `FSWatcher` object will not require the Node.js
event loop to remain active. If there is no other activity keeping the
event loop running, the process may exit before the `FSWatcher` object's
callback is invoked. Calling `watcher.unref()` multiple times will have
no effect.

