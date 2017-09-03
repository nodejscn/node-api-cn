<!-- YAML
added: v0.1.92
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11705
    description: Support for RSASSA-PSS and additional options was added.
-->
- `object` {string | Object}
- `signature` {string | Buffer | TypedArray | DataView}
- `signatureFormat` {string}

Verifies the provided data using the given `object` and `signature`.
The `object` argument can be either a string containing a PEM encoded object,
which can be an RSA public key, a DSA public key, or an X.509 certificate,
or an object with one or more of the following properties:

* `key`: {string} - PEM encoded public key (required)
* `padding`: {integer} - Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  Note that `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to verify the message as specified in section 3.1 of [RFC 4055][].
* `saltLength`: {integer} - salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_AUTO` (default) causes it to be
  determined automatically.

The `signature` argument is the previously calculated signature for the data, in
the `signatureFormat` which can be `'latin1'`, `'hex'` or `'base64'`.
If a `signatureFormat` is specified, the `signature` is expected to be a
string; otherwise `signature` is expected to be a [`Buffer`][],
`TypedArray`, or `DataView`.

Returns `true` or `false` depending on the validity of the signature for
the data and public key.

The `verify` object can not be used again after `verify.verify()` has been
called. Multiple calls to `verify.verify()` will result in an error being
thrown.

