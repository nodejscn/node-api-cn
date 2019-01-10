<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* Returns: {Promise}

Removes the directory identified by `path` then resolves the `Promise` with
no arguments upon success.

Using `fsPromises.rmdir()` on a file (not a directory) results in the
`Promise` being rejected with an `ENOENT` error on Windows and an `ENOTDIR`
error on POSIX.

