<!-- YAML
added: v0.9.3
-->

* `buffer` {Buffer} A `Buffer` containing the bytes to decode.

Returns any remaining input stored in the internal buffer as a string. Bytes
representing incomplete UTF-8 and UTF-16 characters will be replaced with
substitution characters appropriate for the character encoding.

If the `buffer` argument is provided, one final call to `stringDecoder.write()`
is performed before returning the remaining input.

