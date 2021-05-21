<!-- YAML
added: v15.0.0
-->

* Type: {Uint8Array}

The RSA public exponent. This must be a {Uint8Array} containing a big-endian,
unsigned integer that must fit within 32-bits. The {Uint8Array} may contain an
arbitrary number of leading zero-bits. The value must be a prime number. Unless
there is reason to use a different value, use `new Uint8Array([1, 0, 1])`
(65537) as the public exponent.

