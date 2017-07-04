<!-- YAML
added: v0.7.1
-->
- `autoPadding` {boolean} Defaults to `true`.
- Returns the {Cipher} for method chaining.

When data has been encrypted without standard block padding, calling
`decipher.setAutoPadding(false)` will disable automatic padding to prevent
[`decipher.final()`][] from checking for and removing padding.

Turning auto padding off will only work if the input data's length is a
multiple of the ciphers block size.

The `decipher.setAutoPadding()` method must be called before
[`decipher.final()`][].

