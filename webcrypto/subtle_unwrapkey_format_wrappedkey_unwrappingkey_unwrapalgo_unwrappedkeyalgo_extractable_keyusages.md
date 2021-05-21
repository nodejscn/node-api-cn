<!-- YAML
added: v15.0.0
-->

* `format`: {string} Must be one of `'raw'`, `'pkcs8'`, `'spki'`, or `'jwk'`.
* `wrappedKey`: {ArrayBuffer|TypedArray|DataView|Buffer}
* `unwrappingKey`: {CryptoKey}
<!--lint disable maximum-line-length remark-lint-->
* `unwrapAlgo`: {RsaOaepParams|AesCtrParams|AesCbcParams|AesGcmParams|AesKwParams}
* `unwrappedKeyAlgo`: {RsaHashedImportParams|EcKeyImportParams|HmacImportParams|AesImportParams}
<!--lint enable maximum-line-length remark-lint-->
* `extractable`: {boolean}
* `keyUsages`: {string[]} See [Key usages][].
* Returns: {Promise} containing {CryptoKey}

In cryptography, "wrapping a key" refers to exporting and then encrypting the
keying material. The `subtle.unwrapKey()` method attempts to decrypt a wrapped
key and create a {CryptoKey} instance. It is equivalent to calling
`subtle.decrypt()` first on the encrypted key data (using the `wrappedKey`,
`unwrapAlgo`, and `unwrappingKey` arguments as input) then passing the results
in to the `subtle.importKey()` method using the `unwrappedKeyAlgo`,
`extractable`, and `keyUsages` arguments as inputs. If successful, the returned
promise is resolved with a {CryptoKey} object.

The wrapping algorithms currently supported include:

* `'RSA-OAEP'`
* `'AES-CTR'`<sup>1</sup>
* `'AES-CBC'`<sup>1</sup>
* `'AES-GCM'`<sup>1</sup>
* `'AES-KW'`<sup>1</sup>

The unwrapped key algorithms supported include:

* `'RSASSA-PKCS1-v1_5'`
* `'RSA-PSS'`
* `'RSA-OAEP'`
* `'ECDSA'`
* `'ECDH'`
* `'HMAC'`
* `'AES-CTR'`
* `'AES-CBC'`
* `'AES-GCM'`
* `'AES-KW'`
* `'NODE-DSA'`<sup>1</sup>
* `'NODE-DH'`<sup>1</sup>

<sup>1</sup> Non-standard Node.js extension

