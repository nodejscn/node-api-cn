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
  - version: v11.13.0
    pr-url: https://github.com/nodejs/node/pull/26278
    description: The `key` argument can now be a `KeyObject` with type
                 `private`.
  - version: v11.7.0
    pr-url: https://github.com/nodejs/node/pull/25217
    description: The `key` argument can now be a private key.
-->

<!--lint disable maximum-line-length remark-lint-->
* `key` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView}
  * `key`: {string|ArrayBuffer|Buffer|TypedArray|DataView|Object} The key
    material, either in PEM, DER, or JWK format.
  * `format`: {string} Must be `'pem'`, `'der'`, or '`'jwk'`.
    **Default:** `'pem'`.
  * `type`: {string} Must be `'pkcs1'` or `'spki'`. This option is
     required only if the `format` is `'der'` and ignored otherwise.
  * `encoding` {string} The string encoding to use when `key` is a string.
* Returns: {KeyObject}
<!--lint enable maximum-line-length remark-lint-->

Creates and returns a new key object containing a public key. If `key` is a
string or `Buffer`, `format` is assumed to be `'pem'`; if `key` is a `KeyObject`
with type `'private'`, the public key is derived from the given private key;
otherwise, `key` must be an object with the properties described above.

If the format is `'pem'`, the `'key'` may also be an X.509 certificate.

Because public keys can be derived from private keys, a private key may be
passed instead of a public key. In that case, this function behaves as if
[`crypto.createPrivateKey()`][] had been called, except that the type of the
returned `KeyObject` will be `'public'` and that the private key cannot be
extracted from the returned `KeyObject`. Similarly, if a `KeyObject` with type
`'private'` is given, a new `KeyObject` with type `'public'` will be returned
and it will be impossible to extract the private key from the returned object.

