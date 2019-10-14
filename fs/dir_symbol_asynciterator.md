<!-- YAML
added: v12.12.0
-->

* Returns: {AsyncIterator} of {fs.Dirent}

Asynchronously iterates over the directory via readdir(3) until all entries have
been read.

Entries returned by the async iterator are always an [`fs.Dirent`][].
The `null` case from `dir.read()` is handled internally.

See [`fs.Dir`][] for an example.

_Directory entries returned by this iterator are in no particular order as
provided by the operating system's underlying directory mechanisms._

