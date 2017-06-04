<!-- YAML
added: v0.1.94
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `input_encoding` changed from `binary` to `utf8`.
-->
- `data` {string | Buffer | TypedArray | DataView}
- `input_encoding` {string}
- `output_encoding` {string}

Updates the decipher with `data`. If the `input_encoding` argument is given,
its value must be one of `'latin1'`, `'base64'`, or `'hex'` and the `data`
argument is a string using the specified encoding. If the `input_encoding`
argument is not given, `data` must be a [`Buffer`][]. If `data` is a
[`Buffer`][] then `input_encoding` is ignored.

The `output_encoding` specifies the output format of the enciphered
data, and can be `'latin1'`, `'ascii'` or `'utf8'`. If the `output_encoding`
is specified, a string using the specified encoding is returned. If no
`output_encoding` is provided, a [`Buffer`][] is returned.

The `decipher.update()` method can be called multiple times with new data until
[`decipher.final()`][] is called. Calling `decipher.update()` after
[`decipher.final()`][] will result in an error being thrown.

