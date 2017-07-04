<!-- YAML
added: v1.1.0
-->
- `privateKey` {Object | string}
  - `key` {string} A PEM encoded private key.
  - `passphrase` {string} An optional passphrase for the private key.
  - `padding` {crypto.constants} An optional padding value defined in
    `crypto.constants`, which may be: `crypto.constants.RSA_NO_PADDING` or
    `RSA_PKCS1_PADDING`.
- `buffer` {Buffer | TypedArray | DataView}

Encrypts `buffer` with `privateKey`.

`privateKey` can be an object or a string. If `privateKey` is a string, it is
treated as the key with no passphrase and will use `RSA_PKCS1_PADDING`.

