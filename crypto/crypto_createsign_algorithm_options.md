<!-- YAML
added: v0.1.92
-->
- `algorithm` {string}
- `options` {Object} [`stream.Writable` options][]

Creates and returns a `Sign` object that uses the given `algorithm`.
Use [`crypto.getHashes()`][] to obtain an array of names of the available
signing algorithms. Optional `options` argument controls the
`stream.Writable` behavior.

