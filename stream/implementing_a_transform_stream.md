
A [Transform][] stream is a [Duplex][] stream where the output is computed
in some way from the input. Examples include [zlib][] streams or [crypto][]
streams that compress, encrypt, or decrypt data.

*Note*: There is no requirement that the output be the same size as the input,
the same number of chunks, or arrive at the same time. For example, a
Hash stream will only ever have a single chunk of output which is
provided when the input is ended. A `zlib` stream will produce output
that is either much smaller or much larger than its input.

The `stream.Transform` class is extended to implement a [Transform][] stream.

The `stream.Transform` class prototypically inherits from `stream.Duplex` and
implements its own versions of the `writable._write()` and `readable._read()`
methods. Custom Transform implementations *must* implement the
[`transform._transform()`][stream-_transform] method and *may* also implement
the [`transform._flush()`][stream-_flush] method.

*Note*: Care must be taken when using Transform streams in that data written
to the stream can cause the Writable side of the stream to become paused if
the output on the Readable side is not consumed.

