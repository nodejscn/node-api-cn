<!-- YAML
added: v0.1.94
-->
- `algorithm` {string}
- `password` {string | Buffer | TypedArray | DataView}

Creates and returns a `Cipher` object that uses the given `algorithm` and
`password`.

The `algorithm` is dependent on OpenSSL, examples are `'aes192'`, etc. On
recent OpenSSL releases, `openssl list-cipher-algorithms` will display the
available cipher algorithms.

The `password` is used to derive the cipher key and initialization vector (IV).
The value must be either a `'latin1'` encoded string, a [`Buffer`][], a
`TypedArray`, or a `DataView`.

The implementation of `crypto.createCipher()` derives keys using the OpenSSL
function [`EVP_BytesToKey`][] with the digest algorithm set to MD5, one
iteration, and no salt. The lack of salt allows dictionary attacks as the same
password always creates the same key. The low iteration count and
non-cryptographically secure hash algorithm allow passwords to be tested very
rapidly.

In line with OpenSSL's recommendation to use pbkdf2 instead of
[`EVP_BytesToKey`][] it is recommended that developers derive a key and IV on
their own using [`crypto.pbkdf2()`][] and to use [`crypto.createCipheriv()`][]
to create the `Cipher` object.

