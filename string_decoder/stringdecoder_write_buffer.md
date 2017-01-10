<!-- YAML
added: v0.1.99
-->

* `buffer` {Buffer} A `Buffer` containing the bytes to decode.

Returns a decoded string, ensuring that any incomplete multibyte characters at
the end of the `Buffer` are omitted from the returned string and stored in an
internal buffer for the next call to `stringDecoder.write()` or
`stringDecoder.end()`.
