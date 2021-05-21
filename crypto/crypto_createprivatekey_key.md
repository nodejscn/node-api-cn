<!-- YAML
added: v11.6.0
changes:
  - version: v15.12.0
    pr-url: https://github.com/nodejs/node/pull/37254
    description: The key can also be a JWK object.
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The key can also be an ArrayBuffer. The encoding option was
                 added. The key cannot contain more than 2 ** 32 - 1 bytes.
-->

<!--lint disable maximum-line-length remark-lint-->
* `key` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView}
  * `key`: {string|ArrayBuffer|Buffer|TypedArray|DataView|Object} The key
    material, either in PEM, DER, or JWK format.
  * `format`: {string} Must be `'pem'`, `'der'`, or '`'jwk'`.
    **Default:** `'pem'`.
  * `type`: {string} Must be `'pkcs1'`, `'pkcs8'` or `'sec1'`. This option is
     required only if the `format` is `'der'` and ignored otherwise.
  * `passphrase`: {string | Buffer} The passphrase to use for decryption.
  * `encoding`: {string} The string encoding to use when `key` is a string.
* Returns: {KeyObject}
<!--lint enable maximum-line-length remark-lint-->

Creates and returns a new key object containing a private key. If `key` is a
string or `Buffer`, `format` is assumed to be `'pem'`; otherwise, `key`
must be an object with the properties described above.

If the private key is encrypted, a `passphrase` must be specified. The length
of the passphrase is limited to 1024 bytes.

