<!-- YAML
added: v12.0.0
-->

* `algorithm` {string | null | undefined}
* `data` {Buffer | TypedArray | DataView}
* `key` {Object | string | Buffer | KeyObject}
* `signature` {Buffer | TypedArray | DataView}
* Returns: {boolean}

Verifies the given signature for `data` using the given key and algorithm. If
`algorithm` is `null` or `undefined`, then the algorithm is dependent upon the
key type (especially Ed25519 and Ed448).

If `key` is not a [`KeyObject`][], this function behaves as if `key` had been
passed to [`crypto.createPublicKey()`][]. If it is an object, the following
additional properties can be passed:

* `dsaEncoding` {string} For DSA and ECDSA, this option specifies the
  format of the generated signature. It can be one of the following:
  * `'der'` (default): DER-encoded ASN.1 signature structure encoding `(r, s)`.
  * `'ieee-p1363'`: Signature format `r || s` as proposed in IEEE-P1363.
* `padding` {integer} Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to sign the message as specified in section 3.1 of [RFC 4055][].
* `saltLength` {integer} Salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_MAX_SIGN` (default) sets it to the
  maximum permissible value.

The `signature` argument is the previously calculated signature for the `data`.

Because public keys can be derived from private keys, a private key or a public
key may be passed for `key`.

