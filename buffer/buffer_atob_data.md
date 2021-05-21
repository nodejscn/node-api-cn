<!-- YAML
added: v15.13.0
-->

> Stability: 3 - Legacy. Use `Buffer.from(data, 'base64')` instead.

* `data` {any} The Base64-encoded input string.

Decodes a string of Base64-encoded data into bytes, and encodes those bytes
into a string using Latin-1 (ISO-8859-1).

The `data` may be any JavaScript-value that can be coerced into a string.

**This function is only provided for compatibility with legacy web platform APIs
and should never be used in new code, because they use strings to represent
binary data and predate the introduction of typed arrays in JavaScript.
For code running using Node.js APIs, converting between base64-encoded strings
and binary data should be performed using `Buffer.from(str, 'base64')` and
`buf.toString('base64')`.**

