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

Updates the decipher with `data`. If the `inputEncoding` argument is given,
its value must be one of `'latin1'`, `'base64'`, or `'hex'` and the `data`
argument is a string using the specified encoding. If the `inputEncoding`
argument is not given, `data` must be a [`Buffer`][]. If `data` is a
[`Buffer`][] then `inputEncoding` is ignored.

The `outputEncoding` specifies the output format of the enciphered
data, and can be `'latin1'`, `'ascii'` or `'utf8'`. If the `outputEncoding`
is specified, a string using the specified encoding is returned. If no
`outputEncoding` is provided, a [`Buffer`][] is returned.

The `decipher.update()` method can be called multiple times with new data until
[`decipher.final()`][] is called. Calling `decipher.update()` after
[`decipher.final()`][] will result in an error being thrown.

