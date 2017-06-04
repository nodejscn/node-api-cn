<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `input_encoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `input_encoding` {string}

Updates the `Hmac` content with the given `data`, the encoding of which
is given in `input_encoding` and can be `'utf8'`, `'ascii'` or
`'latin1'`. If `encoding` is not provided, and the `data` is a string, an
encoding of `'utf8'` is enforced. If `data` is a [`Buffer`][], `TypedArray`, or
`DataView`, then `input_encoding` is ignored.

This can be called many times with new data as it is streamed.

