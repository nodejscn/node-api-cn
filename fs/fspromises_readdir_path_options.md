<!-- YAML
added: v10.0.0
changes:
  - version: v10.11.0
    pr-url: https://github.com/nodejs/node/pull/22020
    description: New option `withFileTypes` was added.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **Default:** `'utf8'`
  * `withFileTypes` {boolean} **Default:** `false`
* Returns: {Promise}

Reads the contents of a directory then resolves the `Promise` with an array
of the names of the files in the directory excluding `'.'` and `'..'`.

The optional `options` argument can be a string specifying an encoding, or an
object with an `encoding` property specifying the character encoding to use for
the filenames. If the `encoding` is set to `'buffer'`, the filenames returned
will be passed as `Buffer` objects.

If `options.withFileTypes` is set to `true`, the resolved array will contain
[`fs.Dirent`][] objects.

