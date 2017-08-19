<!-- YAML
added: v8.4.0
-->

* `fd` {number} A readable file descriptor
* `headers` {[Headers Object][]}
* `options` {Object}
  * `statCheck` {Function}
  * `getTrailers` {Function} Callback function invoked to collect trailer
    headers.
  * `offset` {number} The offset position at which to begin reading
  * `length` {number} The amount of data from the fd to send

Initiates a response whose data is read from the given file descriptor. No
validation is performed on the given file descriptor. If an error occurs while
attempting to read data using the file descriptor, the `Http2Stream` will be
closed using an `RST_STREAM` frame using the standard `INTERNAL_ERROR` code.

When used, the `Http2Stream` object's Duplex interface will be closed
automatically.

```js
const http2 = require('http2');
const fs = require('fs');

const fd = fs.openSync('/some/file', 'r');

const server = http2.createServer();
server.on('stream', (stream) => {
  const stat = fs.fstatSync(fd);
  const headers = {
    'content-length': stat.size,
    'last-modified': stat.mtime.toUTCString(),
    'content-type': 'text/plain'
  };
  stream.respondWithFD(fd, headers);
});
server.on('close', () => fs.closeSync(fd));
```

The optional `options.statCheck` function may be specified to give user code
an opportunity to set additional content headers based on the `fs.Stat` details
of the given fd. If the `statCheck` function is provided, the
`http2stream.respondWithFD()` method will perform an `fs.fstat()` call to
collect details on the provided file descriptor.

The `offset` and `length` options may be used to limit the response to a
specific range subset. This can be used, for instance, to support HTTP Range
requests.

When set, the `options.getTrailers()` function is called immediately after
queuing the last chunk of payload data to be sent. The callback is passed a
single object (with a `null` prototype) that the listener may used to specify
the trailing header fields to send to the peer.

```js
const http2 = require('http2');
const fs = require('fs');

const fd = fs.openSync('/some/file', 'r');

const server = http2.createServer();
server.on('stream', (stream) => {
  const stat = fs.fstatSync(fd);
  const headers = {
    'content-length': stat.size,
    'last-modified': stat.mtime.toUTCString(),
    'content-type': 'text/plain'
  };
  stream.respondWithFD(fd, headers, {
    getTrailers(trailers) {
      trailers['ABC'] = 'some value to send';
    }
  });
});
server.on('close', () => fs.closeSync(fd));
```

*Note*: The HTTP/1 specification forbids trailers from containing HTTP/2
"pseudo-header" fields (e.g. `':status'`, `':path'`, etc). An `'error'` event
will be emitted if the `getTrailers` callback attempts to set such header
fields.

