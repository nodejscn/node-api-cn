<!-- YAML
added: v0.1.92
changes:
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35093
    description: The privateKey can also be an ArrayBuffer and CryptoKey.
  - version:
     - v13.2.0
     - v12.16.0
    pr-url: https://github.com/nodejs/node/pull/29292
    description: This function now supports IEEE-P1363 DSA and ECDSA signatures.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26960
    description: This function now supports RSA-PSS keys.
  - version: v11.6.0
    pr-url: https://github.com/nodejs/node/pull/24234
    description: This function now supports key objects.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11705
    description: Support for RSASSA-PSS and additional options was added.
-->

<!--lint disable maximum-line-length remark-lint-->
* `privateKey` {Object|string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject|CryptoKey}
  * `dsaEncoding` {string}
  * `padding` {integer}
  * `saltLength` {integer}
* `outputEncoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string}
<!--lint enable maximum-line-length remark-lint-->

Calculates the signature on all the data passed through using either
[`sign.update()`][] or [`sign.write()`][stream-writable-write].

If `privateKey` is not a [`KeyObject`][], this function behaves as if
`privateKey` had been passed to [`crypto.createPrivateKey()`][]. If it is an
object, the following additional properties can be passed:

* `dsaEncoding` {string} For DSA and ECDSA, this option specifies the
  format of the generated signature. It can be one of the following:
  * `'der'` (default): DER-encoded ASN.1 signature structure encoding `(r, s)`.
  * `'ieee-p1363'`: Signature format `r || s` as proposed in IEEE-P1363.
* `padding` {integer} Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to sign the message as specified in section 3.1 of [RFC 4055][], unless
  an MGF1 hash function has been specified as part of the key in compliance with
  section 3.3 of [RFC 4055][].
* `saltLength` {integer} Salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_MAX_SIGN` (default) sets it to the
  maximum permissible value.

If `outputEncoding` is provided a string is returned; otherwise a [`Buffer`][]
is returned.

The `Sign` object can not be again used after `sign.sign()` method has been
called. Multiple calls to `sign.sign()` will result in an error being thrown.

