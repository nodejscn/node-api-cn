
* {Stream}

The `process.stderr` property returns a [Writable][] stream connected to
`stderr` (fd `2`).

Note: `process.stderr` differs from other Node.js streams in important ways,
see [note on process I/O][] for more information.

