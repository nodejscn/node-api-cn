<!-- YAML
added: v0.5.0
-->
- `other_public_key` {string | Buffer | TypedArray | DataView}
- `input_encoding` {string}
- `output_encoding` {string}

Computes the shared secret using `other_public_key` as the other
party's public key and returns the computed shared secret. The supplied
key is interpreted using the specified `input_encoding`, and secret is
encoded using specified `output_encoding`. Encodings can be
`'latin1'`, `'hex'`, or `'base64'`. If the `input_encoding` is not
provided, `other_public_key` is expected to be a [`Buffer`][],
`TypedArray`, or `DataView`.

If `output_encoding` is given a string is returned; otherwise, a
[`Buffer`][] is returned.

