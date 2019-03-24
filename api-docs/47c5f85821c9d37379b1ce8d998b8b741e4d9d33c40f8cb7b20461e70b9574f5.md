<!-- YAML
added: v0.11.14
-->
* `privateKey` {string | Buffer | TypedArray | DataView}
* `encoding` {string} The [encoding][] of the `privateKey` string.

Sets the EC Diffie-Hellman private key.
If `encoding` is provided, `privateKey` is expected
to be a string; otherwise `privateKey` is expected to be a [`Buffer`][],
`TypedArray`, or `DataView`.

If `privateKey` is not valid for the curve specified when the `ECDH` object was
created, an error is thrown. Upon setting the private key, the associated
public point (key) is also generated and set in the `ECDH` object.

