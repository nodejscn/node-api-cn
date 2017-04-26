
There are some cases where it is necessary to trigger a refresh of the
underlying readable stream mechanisms, without actually consuming any
data. In such cases, it is possible to call `readable.read(0)`, which will
always return `null`.

If the internal read buffer is below the `highWaterMark`, and the
stream is not currently reading, then calling `stream.read(0)` will trigger
a low-level [`stream._read()`][stream-_read] call.

While most applications will almost never need to do this, there are
situations within Node.js where this is done, particularly in the
Readable stream class internals.

