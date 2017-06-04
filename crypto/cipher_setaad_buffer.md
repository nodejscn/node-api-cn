<!-- YAML
added: v1.0.0
-->
- `buffer` {Buffer}
- Returns the {Cipher} for method chaining.

When using an authenticated encryption mode (only `GCM` is currently
supported), the `cipher.setAAD()` method sets the value used for the
_additional authenticated data_ (AAD) input parameter.

The `cipher.setAAD()` method must be called before [`cipher.update()`][].

