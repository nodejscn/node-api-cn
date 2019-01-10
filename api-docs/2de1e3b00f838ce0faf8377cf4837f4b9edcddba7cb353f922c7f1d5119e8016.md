<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} See [support of file system `flags`][].
* `mode` {integer} **Default:** `0o666` (readable and writable)
* Returns: {Promise}

Asynchronous file open that returns a `Promise` that, when resolved, yields a
`FileHandle` object. See open(2).

`mode` sets the file mode (permission and sticky bits), but only if the file was
created.

Some characters (`< > : " / \ | ? *`) are reserved under Windows as documented
by [Naming Files, Paths, and Namespaces][]. Under NTFS, if the filename contains
a colon, Node.js will open a file system stream, as described by
[this MSDN page][MSDN-Using-Streams].

