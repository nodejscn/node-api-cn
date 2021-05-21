<!-- YAML
added: v15.0.0
-->

<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {EcdhKeyDeriveParams|HkdfParams|Pbkdf2Params|NodeDhDeriveBitsParams|NodeScryptParams}
* `baseKey`: {CryptoKey}
* `derivedKeyAlgorithm`: {HmacKeyGenParams|AesKeyGenParams}
* `extractable`: {boolean}
* `keyUsages`: {string[]} See [Key usages][].
* Returns: {Promise} containing {CryptoKey}
<!--lint enable maximum-line-length remark-lint-->

Using the method and parameters specified in `algorithm`, and the keying
material provided by `baseKey`, `subtle.deriveKey()` attempts to generate
a new {CryptoKey} based on the method and parameters in `derivedKeyAlgorithm`.

Calling `subtle.deriveKey()` is equivalent to calling `subtle.deriveBits()` to
generate raw keying material, then passing the result into the
`subtle.importKey()` method using the `deriveKeyAlgorithm`, `extractable`, and
`keyUsages` parameters as input.

The algorithms currently supported include:

* `'ECDH'`
* `'HKDF'`
* `'PBKDF2'`
* `'NODE-DH'`<sup>1</sup>
* '`NODE-SCRYPT'`<sup>1</sup>

<sup>1</sup> Node.js-specific extension

