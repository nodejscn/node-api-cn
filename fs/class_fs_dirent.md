<!-- YAML
added: v10.10.0
-->

When [`fs.readdir()`][] or [`fs.readdirSync()`][] is called with the
`withFileTypes` option set to `true`, the resulting array is filled with
`fs.Dirent` objects, rather than strings or `Buffers`.

