<!-- YAML
added: v0.11.14
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/16849
    description: Changed error format to better support invalid public key
                 error
-->
* `otherPublicKey` {string | Buffer | TypedArray | DataView}
* `inputEncoding` {string} The [encoding][] of the `otherPublicKey` string.
* `outputEncoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string}

Computes the shared secret using `otherPublicKey` as the other
party's public key and returns the computed shared secret. The supplied
key is interpreted using specified `inputEncoding`, and the returned secret
is encoded using the specified `outputEncoding`.
If the `inputEncoding` is not
provided, `otherPublicKey` is expected to be a [`Buffer`][], `TypedArray`, or
`DataView`.

If `outputEncoding` is given a string will be returned; otherwise a
[`Buffer`][] is returned.

`ecdh.computeSecret` will throw an
`ERR_CRYPTO_ECDH_INVALID_PUBLIC_KEY` error when `otherPublicKey`
lies outside of the elliptic curve. Since `otherPublicKey` is
usually supplied from a remote user over an insecure network,
its recommended for developers to handle this exception accordingly.

