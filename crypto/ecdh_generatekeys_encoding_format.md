<!-- YAML
added: v0.11.14
-->
- `encoding` {string}
- `format` {string} Defaults to `uncompressed`.

Generates private and public EC Diffie-Hellman key values, and returns
the public key in the specified `format` and `encoding`. This key should be
transferred to the other party.

The `format` argument specifies point encoding and can be `'compressed'` or
`'uncompressed'`. If `format` is not specified, the point will be returned in
`'uncompressed'` format.

The `encoding` argument can be `'latin1'`, `'hex'`, or `'base64'`. If
`encoding` is provided a string is returned; otherwise a [`Buffer`][]
is returned.

