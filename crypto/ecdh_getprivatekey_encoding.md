<!-- YAML
added: v0.11.14
-->
- `encoding` {string}

Returns the EC Diffie-Hellman private key in the specified `encoding`,
which can be `'latin1'`, `'hex'`, or `'base64'`. If `encoding` is provided
a string is returned; otherwise a [`Buffer`][] is returned.

