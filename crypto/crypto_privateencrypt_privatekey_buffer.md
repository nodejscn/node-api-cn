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
* `privateKey` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
  * `key` {string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
    A PEM encoded private key.
  * `passphrase` {string|ArrayBuffer|Buffer|TypedArray|DataView} An optional
    passphrase for the private key.
  * `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING` or
    `crypto.constants.RSA_PKCS1_PADDING`.
  * `encoding` {string} The string encoding to use when `buffer`, `key`,
    or `passphrase` are strings.
* `buffer` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* Returns: {Buffer} A new `Buffer` with the encrypted content.
<!--lint enable maximum-line-length remark-lint-->

Encrypts `buffer` with `privateKey`. The returned data can be decrypted using
the corresponding public key, for example using [`crypto.publicDecrypt()`][].

If `privateKey` is not a [`KeyObject`][], this function behaves as if
`privateKey` had been passed to [`crypto.createPrivateKey()`][]. If it is an
object, the `padding` property can be passed. Otherwise, this function uses
`RSA_PKCS1_PADDING`.

