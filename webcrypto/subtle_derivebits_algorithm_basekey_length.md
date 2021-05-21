<!-- YAML
added: v15.0.0
-->

<!--lint disable maximum-line-length remark-lint-->
* `algorithm`: {EcdhKeyDeriveParams|HkdfParams|Pbkdf2Params|NodeDhDeriveBitsParams|NodeScryptParams}
* `baseKey`: {CryptoKey}
* `length`: {number}
* Returns: {Promise} containing {ArrayBuffer}
<!--lint enable maximum-line-length remark-lint-->

Using the method and parameters specified in `algorithm` and the keying
material provided by `baseKey`, `subtle.deriveBits()` attempts to generate
`length` bits. The Node.js implementation requires that `length` is a
multiple of `8`. If successful, the returned promise will be resolved with
an {ArrayBuffer} containing the generated data.

The algorithms currently supported include:

* `'ECDH'`
* `'HKDF'`
* `'PBKDF2'`
* `'NODE-DH'`<sup>1</sup>
* `'NODE-SCRYPT'`<sup>1</sup>

<sup>1</sup> Node.js-specific extension

