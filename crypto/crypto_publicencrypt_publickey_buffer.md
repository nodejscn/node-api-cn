<!-- YAML
added: v0.11.14
-->
- `publicKey` {Object | string}
  - `key` {string} A PEM encoded private key.
  - `passphrase` {string} An optional passphrase for the private key.
  - `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING`,
    `RSA_PKCS1_PADDING`, or `crypto.constants.RSA_PKCS1_OAEP_PADDING`.
- `buffer` {Buffer | TypedArray | DataView}

Encrypts the content of `buffer` with `publicKey` and returns a new
[`Buffer`][] with encrypted content.

`publicKey` can be an object or a string. If `publicKey` is a string, it is
treated as the key with no passphrase and will use `RSA_PKCS1_OAEP_PADDING`.

Because RSA public keys can be derived from private keys, a private key may
be passed instead of a public key.

