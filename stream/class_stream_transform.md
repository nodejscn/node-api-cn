<!-- YAML
added: v0.9.4
-->

<!--type=class-->

Transform streams are [Duplex][] streams where the output is in some way
related to the input. Like all [Duplex][] streams, Transform streams
implement both the [Readable][] and [Writable][] interfaces.

Examples of Transform streams include:

* [zlib streams][zlib]
* [crypto streams][crypto]


