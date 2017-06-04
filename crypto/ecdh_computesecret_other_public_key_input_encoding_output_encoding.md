<!-- YAML
added: v0.11.14
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5522
    description: The default `input_encoding` changed from `binary` to `utf8`.
-->
- `other_public_key` {string | Buffer | TypedArray | DataView}
- `input_encoding` {string}
- `output_encoding` {string}

Computes the shared secret using `other_public_key` as the other
party's public key and returns the computed shared secret. The supplied
key is interpreted using specified `input_encoding`, and the returned secret
is encoded using the specified `output_encoding`. Encodings can be
`'latin1'`, `'hex'`, or `'base64'`. If the `input_encoding` is not
provided, `other_public_key` is expected to be a [`Buffer`][], `TypedArray`, or
`DataView`.

If `output_encoding` is given a string will be returned; otherwise a
[`Buffer`][] is returned.

