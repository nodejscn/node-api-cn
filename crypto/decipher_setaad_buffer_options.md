<!-- YAML
added: v1.0.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The buffer argument can be a string or ArrayBuffer and is
                limited to no more than 2 ** 31 - 1 bytes.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9398
    description: This method now returns a reference to `decipher`.
-->

* `buffer` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* `options` {Object} [`stream.transform` options][]
  * `plaintextLength` {number}
  * `encoding` {string} String encoding to use when `buffer` is a string.
* Returns: {Decipher} for method chaining.

When using an authenticated encryption mode (`GCM`, `CCM` and `OCB` are
currently supported), the `decipher.setAAD()` method sets the value used for the
_additional authenticated data_ (AAD) input parameter.

The `options` argument is optional for `GCM`. When using `CCM`, the
`plaintextLength` option must be specified and its value must match the length
of the ciphertext in bytes. See [CCM mode][].

The `decipher.setAAD()` method must be called before [`decipher.update()`][].

When passing a string as the `buffer`, please consider
[caveats when using strings as inputs to cryptographic APIs][].

