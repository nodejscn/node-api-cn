<!-- YAML
added: v0.1.94
-->
- `outputEncoding` {string}

Returns any remaining deciphered contents. If `outputEncoding`
parameter is one of `'latin1'`, `'ascii'` or `'utf8'`, a string is returned.
If an `outputEncoding` is not provided, a [`Buffer`][] is returned.

Once the `decipher.final()` method has been called, the `Decipher` object can
no longer be used to decrypt data. Attempts to call `decipher.final()` more
than once will result in an error being thrown.

