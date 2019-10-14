<!-- YAML
added: v12.12.0
-->

* Returns: {fs.Dirent|null}

Synchronously read the next directory entry via readdir(3) as an
[`fs.Dirent`][].

If there are no more directory entries to read, `null` will be returned.

_Directory entries returned by this function are in no particular order as
provided by the operating system's underlying directory mechanisms._

