<!-- YAML
added: v1.0.0
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/9398
    description: This method now returns a reference to `decipher`.
-->
- `buffer` {Buffer | TypedArray | DataView}
- Returns the {Cipher} for method chaining.

When using an authenticated encryption mode (only `GCM` is currently
supported), the `decipher.setAuthTag()` method is used to pass in the
received _authentication tag_. If no tag is provided, or if the cipher text
has been tampered with, [`decipher.final()`][] with throw, indicating that the
cipher text should be discarded due to failed authentication.

The `decipher.setAuthTag()` method must be called before
[`decipher.final()`][].

