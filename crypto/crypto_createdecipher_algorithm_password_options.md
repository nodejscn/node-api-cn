<!-- YAML
added: v0.1.94
deprecated: v10.0.0
-->

> Stability: 0 - Deprecated: Use [`crypto.createDecipheriv()`][] instead.

- `algorithm` {string}
- `password` {string | Buffer | TypedArray | DataView}
- `options` {Object} [`stream.transform` options][]
- Returns: {Decipher}

Creates and returns a `Decipher` object that uses the given `algorithm` and
`password` (key).

The `options` argument controls stream behavior and is optional except when a
cipher in CCM mode is used (e.g. `'aes-128-ccm'`). In that case, the
`authTagLength` option is required and specifies the length of the
authentication tag in bytes, see [CCM mode][].

The implementation of `crypto.createDecipher()` derives keys using the OpenSSL
function [`EVP_BytesToKey`][] with the digest algorithm set to MD5, one
iteration, and no salt. The lack of salt allows dictionary attacks as the same
password always creates the same key. The low iteration count and
non-cryptographically secure hash algorithm allow passwords to be tested very
rapidly.

In line with OpenSSL's recommendation to use a more modern algorithm instead of
[`EVP_BytesToKey`][] it is recommended that developers derive a key and IV on
their own using [`crypto.scrypt()`][] and to use [`crypto.createDecipheriv()`][]
to create the `Decipher` object.

