<!-- YAML
added: v0.1.92
-->

Updates the `Verify` content with the given `data`, the encoding of which
is given in `input_encoding` and can be `'utf8'`, `'ascii'` or
`'latin1'`. If `encoding` is not provided, and the `data` is a string, an
encoding of `'utf8'` is enforced. If `data` is a [`Buffer`][] then
`input_encoding` is ignored.

This can be called many times with new data as it is streamed.

