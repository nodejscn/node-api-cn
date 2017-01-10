<!-- YAML
added: v0.1.29
-->

* `file` {String | Buffer | Integer} filename or file descriptor
* `data` {String | Buffer}
* `options` {Object | String}
  * `encoding` {String | Null} default = `'utf8'`
  * `mode` {Integer} default = `0o666`
  * `flag` {String} default = `'w'`

The synchronous version of [`fs.writeFile()`][]. Returns `undefined`.

