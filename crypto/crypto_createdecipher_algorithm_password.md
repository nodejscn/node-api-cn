<!-- YAML
added: v0.1.94
-->
- `algorithm` {string}
- `password` {string | Buffer | TypedArray | DataView}

Creates and returns a `Decipher` object that uses the given `algorithm` and
`password` (key).

The implementation of `crypto.createDecipher()` derives keys using the OpenSSL
function [`EVP_BytesToKey`][] with the digest algorithm set to MD5, one
iteration, and no salt. The lack of salt allows dictionary attacks as the same
password always creates the same key. The low iteration count and
non-cryptographically secure hash algorithm allow passwords to be tested very
rapidly.

In line with OpenSSL's recommendation to use pbkdf2 instead of
[`EVP_BytesToKey`][] it is recommended that developers derive a key and IV on
their own using [`crypto.pbkdf2()`][] and to use [`crypto.createDecipheriv()`][]
to create the `Decipher` object.

