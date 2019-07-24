<!-- YAML
added: v1.0.0
-->
* `buffer` {Buffer}
* `options` {Object} [`stream.transform` options][]
  - `plaintextLength` {number}
* Returns: {Cipher} for method chaining.

When using an authenticated encryption mode (`GCM`, `CCM` and `OCB` are
currently supported), the `cipher.setAAD()` method sets the value used for the
_additional authenticated data_ (AAD) input parameter.

The `options` argument is optional for `GCM` and `OCB`. When using `CCM`, the
`plaintextLength` option must be specified and its value must match the length
of the plaintext in bytes. See [CCM mode][].

The `cipher.setAAD()` method must be called before [`cipher.update()`][].

