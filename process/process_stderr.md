
* {Stream}

The `process.stderr` property returns a stream connected to
`stderr` (fd `2`). It is a [`net.Socket`][] (which is a [Duplex][]
stream) unless fd `2` refers to a file, in which case it is
a [Writable][] stream.

*Note*: `process.stderr` differs from other Node.js streams in important ways,
see [note on process I/O][] for more information.

