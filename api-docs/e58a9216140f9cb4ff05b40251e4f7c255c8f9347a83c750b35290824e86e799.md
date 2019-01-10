<!-- YAML
added: v10.0.0
-->
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* Returns: {Promise}

Change the file system timestamps of the object referenced by the `FileHandle`
then resolves the `Promise` with no arguments upon success.

This function does not work on AIX versions before 7.1, it will resolve the
`Promise` with an error using code `UV_ENOSYS`.

