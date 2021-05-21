<!-- YAML
added: v15.0.0
-->

<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {RsaSignParams|RsaPssParams|EcdsaParams|HmacParams|NodeDsaSignParams}
* `key`: {CryptoKey}
* `signature`: {ArrayBuffer|TypedArray|DataView|Buffer}
* `data`: {ArrayBuffer|TypedArray|DataView|Buffer}
* Returns: {Promise} containing {boolean}
<!--lint enable maximum-line-length remark-lint-->

Using the method and parameters given in `algorithm` and the keying material
provided by `key`, `subtle.verify()` attempts to verify that `signature` is
a valid cryptographic signature of `data`. The returned promise is resolved
with either `true` or `false`.

The algorithms currently supported include:

* `'RSASSA-PKCS1-v1_5'`
* `'RSA-PSS'`
* `'ECDSA'`
* `'HMAC'`
* `'NODE-DSA'`<sup>1</sup>
* `'NODE-ED25519'`<sup>1</sup>
* `'NODE-ED448'`<sup>1</sup>

<sup>1</sup> Non-standard Node.js extension

