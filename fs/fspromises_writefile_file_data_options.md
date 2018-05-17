<!-- YAML
added: v10.0.0
-->

* `file` {string|Buffer|URL|FileHandle} filename or `FileHandle`
* `data` {string|Buffer|Uint8Array}
* `options` {Object|string}
  * `encoding` {string|null} **Default:** `'utf8'`
  * `mode` {integer} **Default:** `0o666`
  * `flag` {string} See [support of file system `flags`][]. **Default:** `'w'`.
* Returns: {Promise}

Asynchronously writes data to a file, replacing the file if it already exists.
`data` can be a string or a buffer. The `Promise` will be resolved with no
arguments upon success.

The `encoding` option is ignored if `data` is a buffer.

If `options` is a string, then it specifies the encoding.

Any specified `FileHandle` has to support writing.

It is unsafe to use `fsPromises.writeFile()` multiple times on the same file
without waiting for the `Promise` to be resolved (or rejected).

