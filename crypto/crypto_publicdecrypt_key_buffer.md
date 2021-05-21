<!-- YAML
added: v1.1.0
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: Added string, ArrayBuffer, and CryptoKey as allowable key
                 types. The passphrase can be an ArrayBuffer. The buffer can
                 be a string or ArrayBuffer. All types that accept buffers
                 are limited to a maximum of 2 ** 31 - 1 bytes.
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: This function now supports key objects.
-->

<!--lint disable maximum-line-length remark-lint-->
* `key` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
  * `passphrase` {string|ArrayBuffer|Buffer|TypedArray|DataView} An optional
    passphrase for the private key.
  * `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING` or
    `crypto.constants.RSA_PKCS1_PADDING`.
  * `encoding` {string} The string encoding to use when `buffer`, `key`,
    or `passphrase` are strings.
* `buffer` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* Returns: {Buffer} A new `Buffer` with the decrypted content.
<!--lint enable maximum-line-length remark-lint-->

Decrypts `buffer` with `key`.`buffer` was previously encrypted using
the corresponding private key, for example using [`crypto.privateEncrypt()`][].

If `key` is not a [`KeyObject`][], this function behaves as if
`key` had been passed to [`crypto.createPublicKey()`][]. If it is an
object, the `padding` property can be passed. Otherwise, this function uses
`RSA_PKCS1_PADDING`.

Because RSA public keys can be derived from private keys, a private key may
be passed instead of a public key.

