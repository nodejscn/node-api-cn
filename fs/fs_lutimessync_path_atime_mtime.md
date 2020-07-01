<!-- YAML
added: v14.5.0
-->

* `path` {string|Buffer|URL}
* `atime` {number|string|Date}
* `mtime` {number|string|Date}

Change the file system timestamps of the symbolic link referenced by `path`.
Returns `undefined`, or throws an exception when parameters are incorrect or
the operation fails. This is the synchronous version of [`fs.lutimes()`][].

