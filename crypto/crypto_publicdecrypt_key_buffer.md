<!-- YAML
added: v1.1.0
changes:
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: This function now supports key objects.
-->
* `key` {Object | string | Buffer | KeyObject}
  - `passphrase` {string | Buffer} An optional passphrase for the private key.
  - `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING` or
    `crypto.constants.RSA_PKCS1_PADDING`.
* `buffer` {Buffer | TypedArray | DataView}
* Returns: {Buffer} A new `Buffer` with the decrypted content.

Decrypts `buffer` with `key`.`buffer` was previously encrypted using
the corresponding private key, for example using [`crypto.privateEncrypt()`][].

If `key` is not a [`KeyObject`][], this function behaves as if
`key` had been passed to [`crypto.createPublicKey()`][]. If it is an
object, the `padding` property can be passed. Otherwise, this function uses
`RSA_PKCS1_PADDING`.

Because RSA public keys can be derived from private keys, a private key may
be passed instead of a public key.

