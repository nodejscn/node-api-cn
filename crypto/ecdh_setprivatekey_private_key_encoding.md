<!-- YAML
added: v0.11.14
-->

Sets the EC Diffie-Hellman private key. The `encoding` can be `'latin1'`,
`'hex'` or `'base64'`. If `encoding` is provided, `private_key` is expected
to be a string; otherwise `private_key` is expected to be a [`Buffer`][]. If
`private_key` is not valid for the curve specified when the `ECDH` object was
created, an error is thrown. Upon setting the private key, the associated
public point (key) is also generated and set in the ECDH object.

