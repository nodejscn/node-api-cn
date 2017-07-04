<!-- YAML
added: v0.1.92
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}

Updates the hash content with the given `data`, the encoding of which
is given in `inputEncoding` and can be `'utf8'`, `'ascii'` or
`'latin1'`. If `encoding` is not provided, and the `data` is a string, an
encoding of `'utf8'` is enforced. If `data` is a [`Buffer`][], `TypedArray`, or
`DataView`, then `inputEncoding` is ignored.

This can be called many times with new data as it is streamed.

