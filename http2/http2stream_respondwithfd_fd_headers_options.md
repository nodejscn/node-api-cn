<!-- YAML
added: v8.4.0
changes:
  - version: v14.5.0
    pr-url: https://github.com/nodejs/node/pull/33160
    description: Allow explicity setting date headers.
  - version: v12.12.0
    pr-url: https://github.com/nodejs/node/pull/29876
    description: The `fd` option may now be a `FileHandle`.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18936
    description: Any readable file descriptor, not necessarily for a
                 regular file, is supported now.
-->

* `fd` {number|FileHandle} A readable file descriptor.
* `headers` {HTTP/2 Headers Object}
* `options` {Object}
  * `statCheck` {Function}
  * `waitForTrailers` {boolean} When `true`, the `Http2Stream` will emit the
    `'wantTrailers'` event after the final `DATA` frame has been sent.
  * `offset` {number} The offset position at which to begin reading.
  * `length` {number} The amount of data from the fd to send.

Initiates a response whose data is read from the given file descriptor. No
validation is performed on the given file descriptor. If an error occurs while
attempting to read data using the file descriptor, the `Http2Stream` will be
closed using an `RST_STREAM` frame using the standard `INTERNAL_ERROR` code.

When used, the `Http2Stream` object's `Duplex` interface will be closed
automatically.

```js
const http2 = require('http2');
const fs = require('fs');

const server = http2.createServer();
server.on('stream', (stream) => {
  const fd = fs.openSync('/some/file', 'r');

  const stat = fs.fstatSync(fd);
  const headers = {
    'content-length': stat.size,
    'last-modified': stat.mtime.toUTCString(),
    'content-type': 'text/plain; charset=utf-8'
  };
  stream.respondWithFD(fd, headers);
  stream.on('close', () => fs.closeSync(fd));
});
```

The optional `options.statCheck` function may be specified to give user code
an opportunity to set additional content headers based on the `fs.Stat` details
of the given fd. If the `statCheck` function is provided, the
`http2stream.respondWithFD()` method will perform an `fs.fstat()` call to
collect details on the provided file descriptor.

The `offset` and `length` options may be used to limit the response to a
specific range subset. This can be used, for instance, to support HTTP Range
requests.

The file descriptor or `FileHandle` is not closed when the stream is closed,
so it will need to be closed manually once it is no longer needed.
Using the same file descriptor concurrently for multiple streams
is not supported and may result in data loss. Re-using a file descriptor
after a stream has finished is supported.

When the `options.waitForTrailers` option is set, the `'wantTrailers'` event
will be emitted immediately after queuing the last chunk of payload data to be
sent. The `http2stream.sendTrailers()` method can then be used to sent trailing
header fields to the peer.

When `options.waitForTrailers` is set, the `Http2Stream` will not automatically
close when the final `DATA` frame is transmitted. User code *must* call either
`http2stream.sendTrailers()` or `http2stream.close()` to close the
`Http2Stream`.

```js
const http2 = require('http2');
const fs = require('fs');

const server = http2.createServer();
server.on('stream', (stream) => {
  const fd = fs.openSync('/some/file', 'r');

  const stat = fs.fstatSync(fd);
  const headers = {
    'content-length': stat.size,
    'last-modified': stat.mtime.toUTCString(),
    'content-type': 'text/plain; charset=utf-8'
  };
  stream.respondWithFD(fd, headers, { waitForTrailers: true });
  stream.on('wantTrailers', () => {
    stream.sendTrailers({ ABC: 'some value to send' });
  });

  stream.on('close', () => fs.closeSync(fd));
});
```

