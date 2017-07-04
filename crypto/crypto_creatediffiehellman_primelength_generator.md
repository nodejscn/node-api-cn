<!-- YAML
added: v0.5.0
-->
- `primeLength` {number}
- `generator` {number | string | Buffer | TypedArray | DataView} Defaults to `2`.

Creates a `DiffieHellman` key exchange object and generates a prime of
`primeLength` bits using an optional specific numeric `generator`.
If `generator` is not specified, the value `2` is used.

