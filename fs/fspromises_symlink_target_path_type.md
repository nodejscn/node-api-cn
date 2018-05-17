<!-- YAML
added: v10.0.0
-->

* `target` {string|Buffer|URL}
* `path` {string|Buffer|URL}
* `type` {string} **Default:** `'file'`
* Returns: {Promise}

Creates a symbolic link then resolves the `Promise` with no arguments upon
success.

The `type` argument is only used on Windows platforms and can be one of `'dir'`,
`'file'`, or `'junction'`. Note that Windows junction
points require the destination path to be absolute. When using `'junction'`,
the `target` argument will automatically be normalized to absolute path.

