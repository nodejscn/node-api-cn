<!-- YAML
added: v0.11.14
changes:
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

* `privateKey` {Object | string | Buffer | KeyObject}
  * `oaepHash` {string} The hash function to use for OAEP padding.
    **Default:** `'sha1'`
  * `oaepLabel` {Buffer | TypedArray | DataView} The label to use for OAEP
     padding. If not specified, no label is used.
  * `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING`,
    `crypto.constants.RSA_PKCS1_PADDING`, or
    `crypto.constants.RSA_PKCS1_OAEP_PADDING`.
* `buffer` {Buffer | TypedArray | DataView}
* Returns: {Buffer} A new `Buffer` with the decrypted content.

Decrypts `buffer` with `privateKey`. `buffer` was previously encrypted using
the corresponding public key, for example using [`crypto.publicEncrypt()`][].

If `privateKey` is not a [`KeyObject`][], this function behaves as if
`privateKey` had been passed to [`crypto.createPrivateKey()`][]. If it is an
object, the `padding` property can be passed. Otherwise, this function uses
`RSA_PKCS1_OAEP_PADDING`.

