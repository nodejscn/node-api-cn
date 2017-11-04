<!-- YAML
added: v8.0.0
-->

* `err` {Error} A possible error.
* `callback` {Function} A callback function that takes an optional error
  argument.

The `_destroy()` method is called by [`writable.destroy()`][writable-destroy].
It can be overriden by child classes but it **must not** be called directly.
