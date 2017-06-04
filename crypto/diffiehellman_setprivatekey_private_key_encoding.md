<!-- YAML
added: v0.5.0
-->
- `private_key` {string | Buffer | TypedArray | DataView}
- `encoding` {string}

Sets the Diffie-Hellman private key. If the `encoding` argument is provided
and is either `'latin1'`, `'hex'`, or `'base64'`, `private_key` is expected
to be a string. If no `encoding` is provided, `private_key` is expected
to be a [`Buffer`][], `TypedArray`, or `DataView`.

