<!-- YAML
added: v0.1.94
deprecated: v10.0.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The password argument can be an ArrayBuffer and is limited to
                 a maximum of 2 ** 31 - 1 bytes.
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/21447
    description: Ciphers in OCB mode are now supported.
  - version: v10.2.0
    pr-url: https://github.com/nodejs/node/pull/20235
    description: The `authTagLength` option can now be used to produce shorter
                 authentication tags in GCM mode and defaults to 16 bytes.
-->

> Stability: 0 - Deprecated: Use [`crypto.createCipheriv()`][] instead.

* `algorithm` {string}
* `password` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* `options` {Object} [`stream.transform` options][]
* Returns: {Cipher}

Creates and returns a `Cipher` object that uses the given `algorithm` and
`password`.

The `options` argument controls stream behavior and is optional except when a
cipher in CCM or OCB mode is used (e.g. `'aes-128-ccm'`). In that case, the
`authTagLength` option is required and specifies the length of the
authentication tag in bytes, see [CCM mode][]. In GCM mode, the `authTagLength`
option is not required but can be used to set the length of the authentication
tag that will be returned by `getAuthTag()` and defaults to 16 bytes.

The `algorithm` is dependent on OpenSSL, examples are `'aes192'`, etc. On
recent OpenSSL releases, `openssl list -cipher-algorithms`
(`openssl list-cipher-algorithms` for older versions of OpenSSL) will
display the available cipher algorithms.

The `password` is used to derive the cipher key and initialization vector (IV).
The value must be either a `'latin1'` encoded string, a [`Buffer`][], a
`TypedArray`, or a `DataView`.

The implementation of `crypto.createCipher()` derives keys using the OpenSSL
function [`EVP_BytesToKey`][] with the digest algorithm set to MD5, one
iteration, and no salt. The lack of salt allows dictionary attacks as the same
password always creates the same key. The low iteration count and
non-cryptographically secure hash algorithm allow passwords to be tested very
rapidly.

In line with OpenSSL's recommendation to use a more modern algorithm instead of
[`EVP_BytesToKey`][] it is recommended that developers derive a key and IV on
their own using [`crypto.scrypt()`][] and to use [`crypto.createCipheriv()`][]
to create the `Cipher` object. Users should not use ciphers with counter mode
(e.g. CTR, GCM, or CCM) in `crypto.createCipher()`. A warning is emitted when
they are used in order to avoid the risk of IV reuse that causes
vulnerabilities. For the case when IV is reused in GCM, see [Nonce-Disrespecting
Adversaries][] for details.

