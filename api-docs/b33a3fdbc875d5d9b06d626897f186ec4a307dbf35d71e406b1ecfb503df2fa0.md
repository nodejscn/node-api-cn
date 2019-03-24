<!-- YAML
added: v1.0.0
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9398
    description: This method now returns a reference to `decipher`.
-->
* `buffer` {Buffer | TypedArray | DataView}
* `options` {Object} [`stream.transform` options][]
  - `plaintextLength` {number}
* Returns: {Decipher} for method chaining.

When using an authenticated encryption mode (`GCM`, `CCM` and `OCB` are
currently supported), the `decipher.setAAD()` method sets the value used for the
_additional authenticated data_ (AAD) input parameter.

The `options` argument is optional for `GCM`. When using `CCM`, the
`plaintextLength` option must be specified and its value must match the length
of the plaintext in bytes. See [CCM mode][].

The `decipher.setAAD()` method must be called before [`decipher.update()`][].

