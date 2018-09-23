<!-- YAML
added: v1.0.0
changes:
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
cipher text should be discarded due to failed authentication.

Note that this Node.js version does not verify the length of GCM authentication
tags. Such a check *must* be implemented by applications and is crucial to the
authenticity of the encrypted data, otherwise, an attacker can use an
arbitrarily short authentication tag to increase the chances of successfully
passing authentication (up to 0.39%). It is highly recommended to associate one
of the values 16, 15, 14, 13, 12, 8 or 4 bytes with each key, and to only permit
authentication tags of that length, see [NIST SP 800-38D][].

The `decipher.setAuthTag()` method must be called before
[`decipher.final()`][].

