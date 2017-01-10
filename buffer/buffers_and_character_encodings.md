
`Buffer` instances are commonly used to represent sequences of encoded characters
such as UTF-8, UCS2, Base64 or even Hex-encoded data. It is possible to
convert back and forth between `Buffer` instances and ordinary JavaScript strings
by using an explicit character encoding.

Example:

```js
const buf = Buffer.from('hello world', 'ascii');

// Prints: 68656c6c6f20776f726c64
console.log(buf.toString('hex'));

// Prints: aGVsbG8gd29ybGQ=
console.log(buf.toString('base64'));
```

The character encodings currently supported by Node.js include:

* `'ascii'` - for 7-bit ASCII data only. This encoding is fast and will strip
  the high bit if set.

* `'utf8'` - Multibyte encoded Unicode characters. Many web pages and other
  document formats use UTF-8.

* `'utf16le'` - 2 or 4 bytes, little-endian encoded Unicode characters.
  Surrogate pairs (U+10000 to U+10FFFF) are supported.

* `'ucs2'` - Alias of `'utf16le'`.

* `'base64'` - Base64 encoding. When creating a `Buffer` from a string,
  this encoding will also correctly accept "URL and Filename Safe Alphabet" as
  specified in [RFC4648, Section 5].

* `'latin1'` - A way of encoding the `Buffer` into a one-byte encoded string
  (as defined by the IANA in [RFC1345],
  page 63, to be the Latin-1 supplement block and C0/C1 control codes).

* `'binary'` - Alias for `'latin1'`.

* `'hex'` - Encode each byte as two hexadecimal characters.

_Note_: Today's browsers follow the [WHATWG spec] which aliases both 'latin1' and
ISO-8859-1 to win-1252. This means that while doing something like `http.get()`,
if the returned charset is one of those listed in the WHATWG spec it's possible
that the server actually returned win-1252-encoded data, and using `'latin1'`
encoding may incorrectly decode the characters.

