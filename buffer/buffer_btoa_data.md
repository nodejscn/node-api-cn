<!-- YAML
added: v15.13.0
-->

> Stability: 3 - Legacy. Use `buf.toString('base64')` instead.

* `data` {any} An ASCII (Latin1) string.

Decodes a string into bytes using Latin-1 (ISO-8859), and encodes those bytes
into a string using Base64.

The `data` may be any JavaScript-value that can be coerced into a string.

**This function is only provided for compatibility with legacy web platform APIs
and should never be used in new code, because they use strings to represent
binary data and predate the introduction of typed arrays in JavaScript.
For code running using Node.js APIs, converting between base64-encoded strings
and binary data should be performed using `Buffer.from(str, 'base64')` and
`buf.toString('base64')`.**

