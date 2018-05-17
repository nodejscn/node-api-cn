<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `len` {integer} **Default:** `0`
* Returns: {Promise}

Truncates the `path` then resolves the `Promise` with no arguments upon
success. The `path` *must* be a string or `Buffer`.

