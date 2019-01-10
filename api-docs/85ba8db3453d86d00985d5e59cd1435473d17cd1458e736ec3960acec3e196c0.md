<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL|FileHandle} filename or `FileHandle`
* `options` {Object|string}
  * `encoding` {string|null} **Default:** `null`
  * `flag` {string} See [support of file system `flags`][]. **Default:** `'r'`.
* Returns: {Promise}

Asynchronously reads the entire contents of a file.

The `Promise` is resolved with the contents of the file. If no encoding is
specified (using `options.encoding`), the data is returned as a `Buffer`
object. Otherwise, the data will be a string.

If `options` is a string, then it specifies the encoding.

When the `path` is a directory, the behavior of `fsPromises.readFile()` is
platform-specific. On macOS, Linux, and Windows, the promise will be rejected
with an error. On FreeBSD, a representation of the directory's contents will be
returned.

Any specified `FileHandle` has to support reading.

