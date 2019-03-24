<!-- YAML
added: v0.5.0
-->
* `encoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string}

Returns the Diffie-Hellman private key in the specified `encoding`.
If `encoding` is provided a
string is returned; otherwise a [`Buffer`][] is returned.

