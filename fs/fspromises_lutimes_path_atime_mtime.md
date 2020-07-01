<!-- YAML
added: v14.5.0
-->

* `path` {string|Buffer|URL}
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* Returns: {Promise}

Changes the access and modification times of a file in the same way as
[`fsPromises.utimes()`][], with the difference that if the path refers to a
symbolic link, then the link is not dereferenced: instead, the timestamps of
the symbolic link itself are changed.

Upon success, the `Promise` is resolved without arguments.

