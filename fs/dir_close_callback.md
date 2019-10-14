<!-- YAML
added: v12.12.0
-->

* `callback` {Function}
  * `err` {Error}

Asynchronously close the directory's underlying resource handle.
Subsequent reads will result in errors.

The `callback` will be called after the resource handle has been closed.

