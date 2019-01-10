<!-- YAML
added: v10.0.0
-->

A `FileHandle` object is a wrapper for a numeric file descriptor.
Instances of `FileHandle` are distinct from numeric file descriptors
in that, if the `FileHandle` is not explicitly closed using the
`filehandle.close()` method, they will automatically close the file descriptor
and will emit a process warning, thereby helping to prevent memory leaks.

Instances of the `FileHandle` object are created internally by the
`fsPromises.open()` method.

Unlike the callback-based API (`fs.fstat()`, `fs.fchown()`, `fs.fchmod()`, and
so on), a numeric file descriptor is not used by the promise-based API. Instead,
the promise-based API uses the `FileHandle` class in order to help avoid
accidental leaking of unclosed file descriptors after a `Promise` is resolved or
rejected.

