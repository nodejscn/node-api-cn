<!-- YAML
added: v0.11.14
-->

Computes the shared secret using `other_public_key` as the other
party's public key and returns the computed shared secret. The supplied
key is interpreted using specified `input_encoding`, and the returned secret
is encoded using the specified `output_encoding`. Encodings can be
`'latin1'`, `'hex'`, or `'base64'`. If the `input_encoding` is not
provided, `other_public_key` is expected to be a [`Buffer`][].

If `output_encoding` is given a string will be returned; otherwise a
[`Buffer`][] is returned.

