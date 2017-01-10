<!-- YAML
added: v0.11.14
-->

Decrypts `buffer` with `private_key`.

`private_key` can be an object or a string. If `private_key` is a string, it is
treated as the key with no passphrase and will use `RSA_PKCS1_OAEP_PADDING`.
If `private_key` is an object, it is interpreted as a hash object with the
keys:

* `key` : {String} - PEM encoded private key
* `passphrase` : {String} - Optional passphrase for the private key
* `padding` : An optional padding value, one of the following:
  * `crypto.constants.RSA_NO_PADDING`
  * `crypto.constants.RSA_PKCS1_PADDING`
  * `crypto.constants.RSA_PKCS1_OAEP_PADDING`

All paddings are defined in `crypto.constants`.

