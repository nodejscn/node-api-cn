<!-- YAML
added: v10.0.0
-->
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} **Default:** `'utf8'`
  * `mode` {integer} **Default:** `0o666`
  * `flag` {string} See [support of file system `flags`][]. **Default:** `'a'`.
* Returns: {Promise}

Asynchronously append data to this file, creating the file if it does not yet
exist. `data` can be a string or a [`Buffer`][]. The `Promise` will be
resolved with no arguments upon success.

If `options` is a string, then it specifies the encoding.

The `FileHandle` must have been opened for appending.

