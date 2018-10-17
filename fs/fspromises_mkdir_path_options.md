<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **Default:** `false`
  * `mode` {integer} Not supported on Windows. **Default:** `0o777`.
* Returns: {Promise}

Asynchronously creates a directory then resolves the `Promise` with no
arguments upon success.

The optional `options` argument can be an integer specifying mode (permission
and sticky bits), or an object with a `mode` property and a `recursive`
property indicating whether parent folders should be created.

