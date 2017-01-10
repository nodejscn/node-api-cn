<!-- YAML
added: v0.6.7
-->

* `file` {String | Buffer | Number} filename or file descriptor
* `data` {String | Buffer}
* `options` {Object | String}
  * `encoding` {String | Null} default = `'utf8'`
  * `mode` {Integer} default = `0o666`
  * `flag` {String} default = `'a'`

The synchronous version of [`fs.appendFile()`][]. Returns `undefined`.

