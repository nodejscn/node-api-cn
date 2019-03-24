<!-- YAML
added: v0.11.14
-->
* `encoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string} The EC Diffie-Hellman in the specified `encoding`.

If `encoding` is specified, a string is returned; otherwise a [`Buffer`][] is
returned.

