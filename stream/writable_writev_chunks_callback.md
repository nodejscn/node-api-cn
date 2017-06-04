
* `chunks` {Array} The chunks to be written. Each chunk has following
  format: `{ chunk: ..., encoding: ... }`.
* `callback` {Function} A callback function (optionally with an error
  argument) to be invoked when processing is complete for the supplied chunks.

*Note*: This function MUST NOT be called by application code directly. It
should be implemented by child classes, and called only by the internal Writable
class methods only.

The `writable._writev()` method may be implemented in addition to
`writable._write()` in stream implementations that are capable of processing
multiple chunks of data at once. If implemented, the method will be called with
all chunks of data currently buffered in the write queue.

The `writable._writev()` method is prefixed with an underscore because it is
internal to the class that defines it, and should never be called directly by
user programs.

