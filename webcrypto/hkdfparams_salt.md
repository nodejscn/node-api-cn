<!-- YAML
added: v15.0.0
-->

* Type: {ArrayBuffer|TypedArray|DataView|Buffer}

The salt value significantly improves the strength of the HKDF algorithm.
It should be random or pseudorandom and should be the same length as the
output of the digest function (for instance, if using `'SHA-256'` as the
digest, the salt should be 256-bits of random data).

