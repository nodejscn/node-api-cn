<!-- YAML
added: v15.0.0
-->

* `format`: {string} Must be one of `'raw'`, `'pkcs8'`, `'spki'`, or `'jwk'`.
* `key`: {CryptoKey}
* `wrappingKey`: {CryptoKey}
* `wrapAlgo`: {RsaOaepParams|AesCtrParams|AesCbcParams|AesGcmParams|AesKwParams}
* Returns: {Promise} containing {ArrayBuffer}

In cryptography, "wrapping a key" refers to exporting and then encrypting the
keying material. The `subtle.wrapKey()` method exports the keying material into
the format identified by `format`, then encrypts it using the method and
parameters specified by `wrapAlgo` and the keying material provided by
`wrappingKey`. It is the equivalent to calling `subtle.exportKey()` using
`format` and `key` as the arguments, then passing the result to the
`subtle.encrypt()` method using `wrappingKey` and `wrapAlgo` as inputs. If
successful, the returned promise will be resolved with an {ArrayBuffer}
containing the encrypted key data.

The wrapping algorithms currently supported include:

* `'RSA-OAEP'`
* `'AES-CTR'`
* `'AES-CBC'`
* `'AES-GCM'`
* `'AES-KW'`

