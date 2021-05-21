<!-- YAML
added: v15.0.0
-->

<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {RsaSignParams|RsaPssParams|EcdsaParams|HmacParams|NodeDsaSignParams}
* `key`: {CryptoKey}
* `data`: {ArrayBuffer|TypedArray|DataView|Buffer}
* Returns: {Promise} containing {ArrayBuffer}
<!--lint enable maximum-line-length remark-lint-->

Using the method and parameters given by `algorithm` and the keying material
provided by `key`, `subtle.sign()` attempts to generate a cryptographic
signature of `data`. If successful, the returned promise is resolved with
an {ArrayBuffer} containing the generated signature.

The algorithms currently supported include:

* `'RSASSA-PKCS1-v1_5'`
* `'RSA-PSS'`
* `'ECDSA'`
* `'HMAC'`
* `'NODE-DSA'`<sup>1</sup>
* `'NODE-ED25519'`<sup>1</sup>
* `'NODE-ED448'`<sup>1</sup>

<sup>1</sup> Non-standard Node.js extension

