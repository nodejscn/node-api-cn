<!-- YAML
added: v11.6.0
-->

* `key` {Object | string | Buffer}
  * `key`: {string | Buffer} The key material, either in PEM or DER format.
  * `format`: {string} Must be `'pem'` or `'der'`. **Default:** `'pem'`.
  * `type`: {string} Must be `'pkcs1'`, `'pkcs8'` or `'sec1'`. This option is
     required only if the `format` is `'der'` and ignored if it is `'pem'`.
  * `passphrase`: {string | Buffer} The passphrase to use for decryption.
* Returns: {KeyObject}

Creates and returns a new key object containing a private key. If `key` is a
string or `Buffer`, `format` is assumed to be `'pem'`; otherwise, `key`
must be an object with the properties described above.

If the private key is encrypted, a `passphrase` must be specified. The length
of the passphrase is limited to 1024 bytes.

