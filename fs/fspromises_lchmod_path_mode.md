<!-- YAML
deprecated: v10.0.0
-->

* `path` {string|Buffer|URL}
* `mode` {integer}
* Returns: {Promise}

Changes the permissions on a symbolic link then resolves the `Promise` with
no arguments upon success. This method is only implemented on macOS.

