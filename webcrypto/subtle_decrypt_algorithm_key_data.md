<!-- YAML
added: v15.0.0
-->

* `algorithm`: {RsaOaepParams|AesCtrParams|AesCbcParams|AesGcmParams}
* `key`: {CryptoKey}
* `data`: {ArrayBuffer|TypedArray|DataView|Buffer}
* Returns: {Promise} containing {ArrayBuffer}

Using the method and parameters specified in `algorithm` and the keying
material provided by `key`, `subtle.decrypt()` attempts to decipher the
provided `data`. If successful, the returned promise will be resolved with
an {ArrayBuffer} containing the plaintext result.

The algorithms currently supported include:

* `'RSA-OAEP'`
* `'AES-CTR'`
* `'AES-CBC'`
* `'AES-GCM`'

