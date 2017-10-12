<!-- YAML
added: v0.1.94
-->
- `algorithm` {string}
- `password` {string | Buffer | TypedArray | DataView}
- `options` {Object} [`stream.transform` options][]

Creates and returns a `Cipher` object that uses the given `algorithm` and
`password`. Optional `options` argument controls stream behavior.

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
to create the `Cipher` object. Users should not use ciphers with counter mode
(e.g. CTR, GCM or CCM) in `crypto.createCipher()`. A warning is emitted when
they are used in order to avoid the risk of IV reuse that causes
vulnerabilities. For the case when IV is reused in GCM, see [Nonce-Disrespecting
Adversaries][] for details.

