<!-- YAML
added: v1.0.0
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/17825
    description: This method now throws if the GCM tag length is invalid.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9398
    description: This method now returns a reference to `decipher`.
-->

* `buffer` {Buffer | TypedArray | DataView}
* Returns: {Decipher} for method chaining.

When using an authenticated encryption mode (`GCM`, `CCM` and `OCB` are
currently supported), the `decipher.setAuthTag()` method is used to pass in the
received _authentication tag_. If no tag is provided, or if the cipher text
has been tampered with, [`decipher.final()`][] will throw, indicating that the
cipher text should be discarded due to failed authentication. If the tag length
is invalid according to [NIST SP 800-38D][] or does not match the value of the
`authTagLength` option, `decipher.setAuthTag()` will throw an error.

The `decipher.setAuthTag()` method must be called before [`decipher.update()`][]
for `CCM` mode or before [`decipher.final()`][] for `GCM` and `OCB` modes.
`decipher.setAuthTag()` can only be called once.

