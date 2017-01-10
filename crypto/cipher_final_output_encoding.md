<!-- YAML
added: v0.1.94
-->

Returns any remaining enciphered contents. If `output_encoding`
parameter is one of `'latin1'`, `'base64'` or `'hex'`, a string is returned.
If an `output_encoding` is not provided, a [`Buffer`][] is returned.

Once the `cipher.final()` method has been called, the `Cipher` object can no
longer be used to encrypt data. Attempts to call `cipher.final()` more than
once will result in an error being thrown.

