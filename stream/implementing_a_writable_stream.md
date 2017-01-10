
The `stream.Writable` class is extended to implement a [Writable][] stream.

Custom Writable streams *must* call the `new stream.Writable([options])`
constructor and implement the `writable._write()` method. The
`writable._writev()` method *may* also be implemented.

