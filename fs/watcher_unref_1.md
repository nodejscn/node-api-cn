<!-- YAML
added:
  - v14.3.0
  - v12.20.0
-->

* Returns: {fs.StatWatcher}

When called, the active {fs.StatWatcher} object will not require the Node.js
event loop to remain active. If there is no other activity keeping the
event loop running, the process may exit before the {fs.StatWatcher} object's
callback is invoked. Calling `watcher.unref()` multiple times will have
no effect.

