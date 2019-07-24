<!-- YAML
added: v0.5.0
-->
* `encoding` {string} The [encoding][] of the return value.
* Returns: {Buffer | string}

Generates private and public Diffie-Hellman key values, and returns
the public key in the specified `encoding`. This key should be
transferred to the other party.
If `encoding` is provided a string is returned; otherwise a
[`Buffer`][] is returned.

