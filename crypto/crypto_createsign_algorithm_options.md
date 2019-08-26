<!-- YAML
added: v0.1.92
-->
* `algorithm` {string}
* `options` {Object} [`stream.Writable` options][]
* Returns: {Sign}

Creates and returns a `Sign` object that uses the given `algorithm`.  Use
[`crypto.getHashes()`][] to obtain the names of the available digest algorithms.
Optional `options` argument controls the `stream.Writable` behavior.

In some cases, a `Sign` instance can be created using the name of a signature
algorithm, such as `'RSA-SHA256'`, instead of a digest algorithm. This will use
the corresponding digest algorithm. This does not work for all signature
algorithms, such as `'ecdsa-with-SHA256'`, so it is best to always use digest
algorithm names.

