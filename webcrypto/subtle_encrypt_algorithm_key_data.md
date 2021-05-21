<!-- YAML
added: v15.0.0
-->

* `algorithm`: {RsaOaepParams|AesCtrParams|AesCbcParams|AesGcmParams}
* `key`: {CryptoKey}
* Returns: {Promise} containing {ArrayBuffer}

Using the method and parameters specified by `algorithm` and the keying
material provided by `key`, `subtle.encrypt()` attempts to encipher `data`.
If successful, the returned promise is resolved with an {ArrayBuffer}
containing the encrypted result.

The algorithms currently supported include:

* `'RSA-OAEP'`
* `'AES-CTR'`
* `'AES-CBC'`
* `'AES-GCM`'

