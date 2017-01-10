<!-- YAML
added: v0.11.14
-->

Encrypts `buffer` with `public_key`.

`public_key` can be an object or a string. If `public_key` is a string, it is
treated as the key with no passphrase and will use `RSA_PKCS1_OAEP_PADDING`.
If `public_key` is an object, it is interpreted as a hash object with the
keys:

* `key` : {String} - PEM encoded public key
* `passphrase` : {String} - Optional passphrase for the private key
* `padding` : An optional padding value, one of the following:
  * `crypto.constants.RSA_NO_PADDING`
  * `crypto.constants.RSA_PKCS1_PADDING`
  * `crypto.constants.RSA_PKCS1_OAEP_PADDING`

Because RSA public keys can be derived from private keys, a private key may
be passed instead of a public key.

All paddings are defined in `crypto.constants`.

