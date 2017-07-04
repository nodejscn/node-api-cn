<!-- YAML
added: v0.7.1
-->
- `autoPadding` {boolean} Defaults to `true`.
- Returns the {Cipher} for method chaining.

When using block encryption algorithms, the `Cipher` class will automatically
add padding to the input data to the appropriate block size. To disable the
default padding call `cipher.setAutoPadding(false)`.

When `autoPadding` is `false`, the length of the entire input data must be a
multiple of the cipher's block size or [`cipher.final()`][] will throw an Error.
Disabling automatic padding is useful for non-standard padding, for instance
using `0x0` instead of PKCS padding.

The `cipher.setAutoPadding()` method must be called before
[`cipher.final()`][].

