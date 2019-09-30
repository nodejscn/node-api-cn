<!-- YAML
added: v11.6.0
-->

* `options`: {Object}
* Returns: {string | Buffer}

For symmetric keys, this function allocates a `Buffer` containing the key
material and ignores any options.

For asymmetric keys, the `options` parameter is used to determine the export
format.

For public keys, the following encoding options can be used:

* `type`: {string} Must be one of `'pkcs1'` (RSA only) or `'spki'`.
* `format`: {string} Must be `'pem'` or `'der'`.

For private keys, the following encoding options can be used:

* `type`: {string} Must be one of `'pkcs1'` (RSA only), `'pkcs8'` or
  `'sec1'` (EC only).
* `format`: {string} Must be `'pem'` or `'der'`.
* `cipher`: {string} If specified, the private key will be encrypted with
   the given `cipher` and `passphrase` using PKCS#5 v2.0 password based
   encryption.
* `passphrase`: {string | Buffer} The passphrase to use for encryption, see
  `cipher`.

When PEM encoding was selected, the result will be a string, otherwise it will
be a buffer containing the data encoded as DER.

PKCS#1, SEC1, and PKCS#8 type keys can be encrypted by using a combination of
the `cipher` and `format` options. The PKCS#8 `type` can be used with any
`format` to encrypt any key algorithm (RSA, EC, or DH) by specifying a
`cipher`. PKCS#1 and SEC1 can only be encrypted by specifying a `cipher`
when the PEM `format` is used. For maximum compatibility, use PKCS#8 for
encrypted private keys. Since PKCS#8 defines its own
encryption mechanism, PEM-level encryption is not supported when encrypting
a PKCS#8 key. See [RFC 5208][] for PKCS#8 encryption and [RFC 1421][] for
PKCS#1 and SEC1 encryption.

