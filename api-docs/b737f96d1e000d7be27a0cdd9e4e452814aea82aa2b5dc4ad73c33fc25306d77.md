<!-- YAML
added: v0.11.14
-->
* `encoding` {string} The [encoding][] of the return value.
* `format` {string} **Default:** `'uncompressed'`
* Returns: {Buffer | string} The EC Diffie-Hellman public key in the specified
  `encoding` and `format`.

The `format` argument specifies point encoding and can be `'compressed'` or
`'uncompressed'`. If `format` is not specified the point will be returned in
`'uncompressed'` format.

If `encoding` is specified, a string is returned; otherwise a [`Buffer`][] is
returned.

