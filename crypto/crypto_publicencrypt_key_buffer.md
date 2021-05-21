<!-- YAML
added: v0.11.14
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: Added string, ArrayBuffer, and CryptoKey as allowable key
                 types. The oaepLabel and passphrase can be ArrayBuffers. The
                 buffer can be a string or ArrayBuffer. All types that accept
                 buffers are limited to a maximum of 2 ** 31 - 1 bytes.
  - version: v12.11.0
    pr-url: https://github.com/nodejs/node/pull/29489
    description: The `oaepLabel` option was added.
  - version: v12.9.0
    pr-url: https://github.com/nodejs/node/pull/28335
    description: The `oaepHash` option was added.
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: This function now supports key objects.
-->

<!--lint disable maximum-line-length remark-lint-->
* `key` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
  * `key` {string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
    A PEM encoded public or private key, {KeyObject}, or {CryptoKey}.
  * `oaepHash` {string} The hash function to use for OAEP padding and MGF1.
    **Default:** `'sha1'`
  * `oaepLabel` {string|ArrayBuffer|Buffer|TypedArray|DataView} The label to
    use for OAEP padding. If not specified, no label is used.
  * `passphrase` {string|ArrayBuffer|Buffer|TypedArray|DataView} An optional
    passphrase for the private key.
  * `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING`,
    `crypto.constants.RSA_PKCS1_PADDING`, or
    `crypto.constants.RSA_PKCS1_OAEP_PADDING`.
  * `encoding` {string} The string encoding to use when `buffer`, `key`,
    `oaepLabel`, or `passphrase` are strings.
* `buffer` {string|ArrayBuffer|Buffer|TypedArray|DataView}
* Returns: {Buffer} A new `Buffer` with the encrypted content.
<!--lint enable maximum-line-length remark-lint-->

Encrypts the content of `buffer` with `key` and returns a new
[`Buffer`][] with encrypted content. The returned data can be decrypted using
the corresponding private key, for example using [`crypto.privateDecrypt()`][].

If `key` is not a [`KeyObject`][], this function behaves as if
`key` had been passed to [`crypto.createPublicKey()`][]. If it is an
object, the `padding` property can be passed. Otherwise, this function uses
`RSA_PKCS1_OAEP_PADDING`.

Because RSA public keys can be derived from private keys, a private key may
be passed instead of a public key.

