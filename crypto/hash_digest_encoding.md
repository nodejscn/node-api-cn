<!-- YAML
added: v0.1.92
-->
- `encoding` {string}

Calculates the digest of all of the data passed to be hashed (using the
[`hash.update()`][] method). The `encoding` can be `'hex'`, `'latin1'` or
`'base64'`. If `encoding` is provided a string will be returned; otherwise
a [`Buffer`][] is returned.

The `Hash` object can not be used again after `hash.digest()` method has been
called. Multiple calls will cause an error to be thrown.

