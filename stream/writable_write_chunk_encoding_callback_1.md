
* `chunk` {Buffer|string|any} The chunk to be written. Will **always**
  be a buffer unless the `decodeStrings` option was set to `false`
  or the stream is operating in object mode.
* `encoding` {string} If the chunk is a string, then `encoding` is the
  character encoding of that string. If chunk is a `Buffer`, or if the
  stream is operating in object mode, `encoding` may be ignored.
* `callback` {Function} Call this function (optionally with an error
  argument) when processing is complete for the supplied chunk.

All Writable stream implementations must provide a
[`writable._write()`][stream-_write] method to send data to the underlying
resource.

*Note*: [Transform][] streams provide their own implementation of the
[`writable._write()`][stream-_write].

*Note*: This function MUST NOT be called by application code directly. It
should be implemented by child classes, and called only by the internal Writable
class methods only.

The `callback` method must be called to signal either that the write completed
successfully or failed with an error. The first argument passed to the
`callback` must be the `Error` object if the call failed or `null` if the
write succeeded.

It is important to note that all calls to `writable.write()` that occur between
the time `writable._write()` is called and the `callback` is called will cause
the written data to be buffered. Once the `callback` is invoked, the stream will
emit a [`'drain'`][] event. If a stream implementation is capable of processing
multiple chunks of data at once, the `writable._writev()` method should be
implemented.

If the `decodeStrings` property is set in the constructor options, then
`chunk` may be a string rather than a Buffer, and `encoding` will
indicate the character encoding of the string. This is to support
implementations that have an optimized handling for certain string
data encodings. If the `decodeStrings` property is explicitly set to `false`,
the `encoding` argument can be safely ignored, and `chunk` will remain the same
object that is passed to `.write()`.

The `writable._write()` method is prefixed with an underscore because it is
internal to the class that defines it, and should never be called directly by
user programs.

