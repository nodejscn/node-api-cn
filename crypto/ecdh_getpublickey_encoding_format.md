<!-- YAML
added: v0.11.14
-->

Returns the EC Diffie-Hellman public key in the specified `encoding` and
`format`.

The `format` argument specifies point encoding and can be `'compressed'`,
`'uncompressed'`, or `'hybrid'`. If `format` is not specified the point will be
returned in `'uncompressed'` format.

The `encoding` argument can be `'latin1'`, `'hex'`, or `'base64'`. If
`encoding` is specified, a string is returned; otherwise a [`Buffer`][] is
returned.

