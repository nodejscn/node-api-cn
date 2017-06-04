
A [Duplex][] stream is one that implements both [Readable][] and [Writable][],
such as a TCP socket connection.

Because JavaScript does not have support for multiple inheritance, the
`stream.Duplex` class is extended to implement a [Duplex][] stream (as opposed
to extending the `stream.Readable` *and* `stream.Writable` classes).

*Note*: The `stream.Duplex` class prototypically inherits from
`stream.Readable` and parasitically from `stream.Writable`, but `instanceof`
will work properly for both base classes due to overriding
[`Symbol.hasInstance`][] on `stream.Writable`.

Custom Duplex streams *must* call the `new stream.Duplex([options])`
constructor and implement *both* the `readable._read()` and
`writable._write()` methods.

