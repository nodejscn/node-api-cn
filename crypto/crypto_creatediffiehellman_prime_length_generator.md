<!-- YAML
added: v0.5.0
-->
- `prime_length` {number}
- `generator` {number | string | Buffer | TypedArray | DataView} Defaults to `2`.

Creates a `DiffieHellman` key exchange object and generates a prime of
`prime_length` bits using an optional specific numeric `generator`.
If `generator` is not specified, the value `2` is used.

