<!-- YAML
added: v0.1.8
-->

* `file` {String | Buffer | Integer} filename or file descriptor
* `options` {Object | String}
  * `encoding` {String | Null} default = `null`
  * `flag` {String} default = `'r'`

Synchronous version of [`fs.readFile`][]. Returns the contents of the `file`.

If the `encoding` option is specified then this function returns a
string. Otherwise it returns a buffer.

