<!-- YAML
added: v0.1.21
-->

* `path` {String | Buffer}

Synchronous version of [`fs.exists()`][].
Returns `true` if the file exists, `false` otherwise.

Note that `fs.exists()` is deprecated, but `fs.existsSync()` is not.
(The `callback` parameter to `fs.exists()` accepts parameters that are
inconsistent with other Node.js callbacks. `fs.existsSync()` does not use
a callback.)

