<!-- YAML
added: v0.1.92
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11705
    description: Support for RSASSA-PSS and additional options was added.
-->
- `privateKey` {string | Object}
  - `key` {string}
  - `passphrase` {string}
- `outputFormat` {string}

Calculates the signature on all the data passed through using either
[`sign.update()`][] or [`sign.write()`][stream-writable-write].

The `privateKey` argument can be an object or a string. If `privateKey` is a
string, it is treated as a raw key with no passphrase. If `privateKey` is an
object, it must contain one or more of the following properties:

* `key`: {string} - PEM encoded private key (required)
* `passphrase`: {string} - passphrase for the private key
* `padding`: {integer} - Optional padding value for RSA, one of the following:
  * `crypto.constants.RSA_PKCS1_PADDING` (default)
  * `crypto.constants.RSA_PKCS1_PSS_PADDING`

  Note that `RSA_PKCS1_PSS_PADDING` will use MGF1 with the same hash function
  used to sign the message as specified in section 3.1 of [RFC 4055][].
* `saltLength`: {integer} - salt length for when padding is
  `RSA_PKCS1_PSS_PADDING`. The special value
  `crypto.constants.RSA_PSS_SALTLEN_DIGEST` sets the salt length to the digest
  size, `crypto.constants.RSA_PSS_SALTLEN_MAX_SIGN` (default) sets it to the
  maximum permissible value.

The `outputFormat` can specify one of `'latin1'`, `'hex'` or `'base64'`. If
`outputFormat` is provided a string is returned; otherwise a [`Buffer`][] is
returned.

The `Sign` object can not be again used after `sign.sign()` method has been
called. Multiple calls to `sign.sign()` will result in an error being thrown.

