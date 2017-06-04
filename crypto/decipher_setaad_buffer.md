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
supported), the `decipher.setAAD()` method sets the value used for the
_additional authenticated data_ (AAD) input parameter.

The `decipher.setAAD()` method must be called before [`decipher.update()`][].

