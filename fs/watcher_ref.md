<!-- YAML
added:
  - v14.3.0
  - v12.20.0
-->

* Returns: {fs.FSWatcher}

When called, requests that the Node.js event loop *not* exit so long as the
{fs.FSWatcher} is active. Calling `watcher.ref()` multiple times will have
no effect.

By default, all {fs.FSWatcher} objects are "ref'ed", making it normally
unnecessary to call `watcher.ref()` unless `watcher.unref()` had been
called previously.

