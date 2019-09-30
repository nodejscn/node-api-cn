<!-- YAML
added: v12.0.0
-->

* `algorithm` {string | null | undefined}
* `data` {Buffer | TypedArray | DataView}
* `key` {Object | string | Buffer | KeyObject}
* Returns: {Buffer}

Calculates and returns the signature for `data` using the given private key and
algorithm. If `algorithm` is `null` or `undefined`, then the algorithm is
dependent upon the key type (especially Ed25519 and Ed448).

If `key` is not a [`KeyObject`][], this function behaves as if `key` had been
passed to [`crypto.createPrivateKey()`][]. If it is an object, the following
additional properties can be passed:

* `padding`: {integer} - Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to sign the message as specified in section 3.1 of [RFC 4055][].
* `saltLength`: {integer} - salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_MAX_SIGN` (default) sets it to the
  maximum permissible value.

