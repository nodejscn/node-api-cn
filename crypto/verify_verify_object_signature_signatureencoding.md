<!-- YAML
added: v0.1.92
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26960
    description: This function now supports RSA-PSS keys.
  - version: v11.7.0
    pr-url: https://github.com/nodejs/node/pull/25217
    description: The key can now be a private key.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11705
    description: Support for RSASSA-PSS and additional options was added.
-->
* `object` {Object | string | Buffer | KeyObject}
  - `padding` {integer}
  - `saltLength` {integer}
* `signature` {string | Buffer | TypedArray | DataView}
* `signatureEncoding` {string} The [encoding][] of the `signature` string.
* Returns: {boolean} `true` or `false` depending on the validity of the
  signature for the data and public key.

Verifies the provided data using the given `object` and `signature`.

If `object` is not a [`KeyObject`][], this function behaves as if
`object` had been passed to [`crypto.createPublicKey()`][]. If it is an
object, the following additional properties can be passed:

* `padding`: {integer} - Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to verify the message as specified in section 3.1 of [RFC 4055][], unless
  an MGF1 hash function has been specified as part of the key in compliance with
  section 3.3 of [RFC 4055][].
* `saltLength`: {integer} - salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_AUTO` (default) causes it to be
  determined automatically.

The `signature` argument is the previously calculated signature for the data, in
the `signatureEncoding`.
If a `signatureEncoding` is specified, the `signature` is expected to be a
string; otherwise `signature` is expected to be a [`Buffer`][],
`TypedArray`, or `DataView`.

The `verify` object can not be used again after `verify.verify()` has been
called. Multiple calls to `verify.verify()` will result in an error being
thrown.

Because public keys can be derived from private keys, a private key may
be passed instead of a public key.

