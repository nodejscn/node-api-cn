
* `callback` {Function} A callback function (optionally with an error
  argument and data) to be called when remaining data has been flushed.

*Note*: This function MUST NOT be called by application code directly. It
should be implemented by child classes, and called only by the internal Readable
class methods only.

In some cases, a transform operation may need to emit an additional bit of
data at the end of the stream. For example, a `zlib` compression stream will
store an amount of internal state used to optimally compress the output. When
the stream ends, however, that additional data needs to be flushed so that the
compressed data will be complete.

Custom [Transform][] implementations *may* implement the `transform._flush()`
method. This will be called when there is no more written data to be consumed,
but before the [`'end'`][] event is emitted signaling the end of the
[Readable][] stream.

Within the `transform._flush()` implementation, the `readable.push()` method
may be called zero or more times, as appropriate. The `callback` function must
be called when the flush operation is complete.

The `transform._flush()` method is prefixed with an underscore because it is
internal to the class that defines it, and should never be called directly by
user programs.

