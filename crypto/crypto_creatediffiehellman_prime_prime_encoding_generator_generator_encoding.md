<!-- YAML
added: v0.11.12
-->

Creates a `DiffieHellman` key exchange object using the supplied `prime` and an
optional specific `generator`.

The `generator` argument can be a number, string, or [`Buffer`][]. If
`generator` is not specified, the value `2` is used.

The `prime_encoding` and `generator_encoding` arguments can be `'latin1'`,
`'hex'`, or `'base64'`.

If `prime_encoding` is specified, `prime` is expected to be a string; otherwise
a [`Buffer`][] is expected.

If `generator_encoding` is specified, `generator` is expected to be a string;
otherwise either a number or [`Buffer`][] is expected.

