<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **Default:** `'utf8'`
* Returns: {Promise}

Determines the actual location of `path` using the same semantics as the
`fs.realpath.native()` function then resolves the `Promise` with the resolved
path.

Only paths that can be converted to UTF8 strings are supported.

The optional `options` argument can be a string specifying an encoding, or an
object with an `encoding` property specifying the character encoding to use for
the path. If the `encoding` is set to `'buffer'`, the path returned will be
passed as a `Buffer` object.

On Linux, when Node.js is linked against musl libc, the procfs file system must
be mounted on `/proc` in order for this function to work. Glibc does not have
this restriction.

