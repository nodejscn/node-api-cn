
The `stream.Readable` class is extended to implement a [Readable][] stream.

Custom Readable streams *must* call the `new stream.Readable([options])`
constructor and implement the `readable._read()` method.

