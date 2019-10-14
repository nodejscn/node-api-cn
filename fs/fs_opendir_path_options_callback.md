<!-- YAML
added: v12.12.0
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `encoding` {string|null} **Default:** `'utf8'`
* `callback` {Function}
  * `err` {Error}
  * `dir` {fs.Dir}

Asynchronously open a directory. See opendir(3).

Creates an [`fs.Dir`][], which contains all further functions for reading from
and cleaning up the directory.

The `encoding` option sets the encoding for the `path` while opening the
directory and subsequent read operations.

