<!-- YAML
added: v0.1.31
-->

* `filename` {String | Buffer}
* `listener` {Function}

Stop watching for changes on `filename`. If `listener` is specified, only that
particular listener is removed. Otherwise, *all* listeners are removed and you
have effectively stopped watching `filename`.

Calling `fs.unwatchFile()` with a filename that is not being watched is a
no-op, not an error.

_Note: [`fs.watch()`][] is more efficient than `fs.watchFile()` and `fs.unwatchFile()`.
`fs.watch()` should be used instead of `fs.watchFile()` and `fs.unwatchFile()`
when possible._

