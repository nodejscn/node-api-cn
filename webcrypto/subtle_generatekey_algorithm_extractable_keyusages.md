<!-- YAML
added: v15.0.0
-->

<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {RsaHashedKeyGenParams|EcKeyGenParams|HmacKeyGenParams|AesKeyGenParams|NodeDsaKeyGenParams|NodeDhKeyGenParams|NodeEdKeyGenParams}
<!--lint enable maximum-line-length remark-lint-->
* `extractable`: {boolean}
* `keyUsages`: {string[]} See [Key usages][].
* Returns: {Promise} containing {CryptoKey|CryptoKeyPair}

Using the method and parameters provided in `algorithm`, `subtle.generateKey()`
attempts to generate new keying material. Depending the method used, the method
may generate either a single {CryptoKey} or a {CryptoKeyPair}.

The {CryptoKeyPair} (public and private key) generating algorithms supported
include:

* `'RSASSA-PKCS1-v1_5'`
* `'RSA-PSS'`
* `'RSA-OAEP'`
* `'ECDSA'`
* `'ECDH'`
* `'NODE-DSA'` <sup>1</sup>
* `'NODE-DH'` <sup>1</sup>
* `'NODE-ED25519'` <sup>1</sup>
* `'NODE-ED448'` <sup>1</sup>

The {CryptoKey} (secret key) generating algorithms supported include:

* `'HMAC'`
* `'AES-CTR'`
* `'AES-CBC'`
* `'AES-GCM'`
* `'AES-KW'`

<sup>1</sup> Non-standard Node.js extension

