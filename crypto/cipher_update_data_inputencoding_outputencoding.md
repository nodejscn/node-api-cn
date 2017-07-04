<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}
- `outputEncoding` {string}

Updates the cipher with `data`. If the `inputEncoding` argument is given,
its value must be one of `'utf8'`, `'ascii'`, or `'latin1'` and the `data`
argument is a string using the specified encoding. If the `inputEncoding`
argument is not given, `data` must be a [`Buffer`][], `TypedArray`, or
`DataView`.  If `data` is a [`Buffer`][], `TypedArray`, or `DataView`, then
`inputEncoding` is ignored.

The `outputEncoding` specifies the output format of the enciphered
data, and can be `'latin1'`, `'base64'` or `'hex'`. If the `outputEncoding`
is specified, a string using the specified encoding is returned. If no
`outputEncoding` is provided, a [`Buffer`][] is returned.

The `cipher.update()` method can be called multiple times with new data until
[`cipher.final()`][] is called. Calling `cipher.update()` after
[`cipher.final()`][] will result in an error being thrown.

