<!-- YAML
added: v0.11.14
-->
* `encoding` {string} The [encoding][] of the return value.
* `format` {string} **Default:** `'uncompressed'`
* Returns: {Buffer | string}

Generates private and public EC Diffie-Hellman key values, and returns
the public key in the specified `format` and `encoding`. This key should be
transferred to the other party.

The `format` argument specifies point encoding and can be `'compressed'` or
`'uncompressed'`. If `format` is not specified, the point will be returned in
`'uncompressed'` format.

If `encoding` is provided a string is returned; otherwise a [`Buffer`][]
is returned.

