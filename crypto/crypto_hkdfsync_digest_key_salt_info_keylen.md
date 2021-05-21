<!-- YAML
added: v15.0.0
-->

* `digest` {string} The digest algorithm to use.
* `key` {string|ArrayBuffer|Buffer|TypedArray|DataView|KeyObject} The secret
  key. It must be at least one byte in length.
* `salt` {string|ArrayBuffer|Buffer|TypedArray|DataView} The salt value. Must
  be provided but can be zero-length.
* `info` {string|ArrayBuffer|Buffer|TypedArray|DataView} Additional info value.
  Must be provided but can be zero-length, and cannot be more than 1024 bytes.
* `keylen` {number} The length of the key to generate. Must be greater than 0.
  The maximum allowable value is `255` times the number of bytes produced by
  the selected digest function (e.g. `sha512` generates 64-byte hashes, making
  the maximum HKDF output 16320 bytes).
* Returns: {ArrayBuffer}

Provides a synchronous HKDF key derivation function as defined in RFC 5869. The
given `key`, `salt` and `info` are used with the `digest` to derive a key of
`keylen` bytes.

The successfully generated `derivedKey` will be returned as an {ArrayBuffer}.

An error will be thrown if any of the input aguments specify invalid values or
types, or if the derived key cannot be generated.

```mjs
const {
  hkdfSync,
} = await import('crypto');

const derivedKey = hkdfSync('sha512', 'key', 'salt', 'info', 64);
console.log(Buffer.from(derivedKey).toString('hex'));  // '24156e2...5391653'
```

```cjs
const {
  hkdfSync,
} = require('crypto');

const derivedKey = hkdfSync('sha512', 'key', 'salt', 'info', 64);
console.log(Buffer.from(derivedKey).toString('hex'));  // '24156e2...5391653'
```

