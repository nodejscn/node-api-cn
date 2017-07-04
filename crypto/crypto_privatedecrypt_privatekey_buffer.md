<!-- YAML
added: v0.11.14
-->
- `privateKey` {Object | string}
  - `key` {string} A PEM encoded private key.
  - `passphrase` {string} An optional passphrase for the private key.
  - `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING`,
    `RSA_PKCS1_PADDING`, or `crypto.constants.RSA_PKCS1_OAEP_PADDING`.
- `buffer` {Buffer | TypedArray | DataView}

Decrypts `buffer` with `privateKey`.

`privateKey` can be an object or a string. If `privateKey` is a string, it is
treated as the key with no passphrase and will use `RSA_PKCS1_OAEP_PADDING`.

