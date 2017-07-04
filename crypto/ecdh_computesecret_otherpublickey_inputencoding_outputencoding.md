<!-- YAML
added: v0.11.14
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `inputEncoding` changed from `binary` to `utf8`.
-->
- `otherPublicKey` {string | Buffer | TypedArray | DataView}
- `inputEncoding` {string}
- `outputEncoding` {string}

Computes the shared secret using `otherPublicKey` as the other
party's public key and returns the computed shared secret. The supplied
key is interpreted using specified `inputEncoding`, and the returned secret
is encoded using the specified `outputEncoding`. Encodings can be
`'latin1'`, `'hex'`, or `'base64'`. If the `inputEncoding` is not
provided, `otherPublicKey` is expected to be a [`Buffer`][], `TypedArray`, or
`DataView`.

If `outputEncoding` is given a string will be returned; otherwise a
[`Buffer`][] is returned.

