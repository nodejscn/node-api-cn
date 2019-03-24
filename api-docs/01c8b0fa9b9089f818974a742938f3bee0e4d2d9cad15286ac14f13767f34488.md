<!-- YAML
added: v0.5.0
-->
* `publicKey` {string | Buffer | TypedArray | DataView}
* `encoding` {string} The [encoding][] of the `publicKey` string.

Sets the Diffie-Hellman public key. If the `encoding` argument is provided,
`publicKey` is expected
to be a string. If no `encoding` is provided, `publicKey` is expected
to be a [`Buffer`][], `TypedArray`, or `DataView`.

