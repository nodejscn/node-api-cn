<!-- YAML
added: v8.4.0
-->

* `path` {string|Buffer|URL}
* `headers` {[Headers Object][]}
* `options` {Object}
  * `statCheck` {Function}
  * `getTrailers` {Function} Callback function invoked to collect trailer
    headers.
  * `offset` {number} The offset position at which to begin reading
  * `length` {number} The amount of data from the fd to send

Sends a regular file as the response. The `path` must specify a regular file
or an `'error'` event will be emitted on the `Http2Stream` object.

When used, the `Http2Stream` object's Duplex interface will be closed
automatically.

The optional `options.statCheck` function may be specified to give user code
an opportunity to set additional content headers based on the `fs.Stat` details
of the given file:

If an error occurs while attempting to read the file data, the `Http2Stream`
will be closed using an `RST_STREAM` frame using the standard `INTERNAL_ERROR`
code.

Example using a file path:

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  function statCheck(stat, headers) {
    headers['last-modified'] = stat.mtime.toUTCString();
  }
  stream.respondWithFile('/some/file',
                         { 'content-type': 'text/plain' },
                         { statCheck });
});
```

The `options.statCheck` function may also be used to cancel the send operation
by returning `false`. For instance, a conditional request may check the stat
results to determine if the file has been modified to return an appropriate
`304` response:

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  function statCheck(stat, headers) {
    // Check the stat here...
    stream.respond({ ':status': 304 });
    return false; // Cancel the send operation
  }
  stream.respondWithFile('/some/file',
                         { 'content-type': 'text/plain' },
                         { statCheck });
});
```

The `content-length` header field will be automatically set.

The `offset` and `length` options may be used to limit the response to a
specific range subset. This can be used, for instance, to support HTTP Range
requests.

When set, the `options.getTrailers()` function is called immediately after
queuing the last chunk of payload data to be sent. The callback is passed a
single object (with a `null` prototype) that the listener may used to specify
the trailing header fields to send to the peer.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream) => {
  function getTrailers(trailers) {
    trailers['ABC'] = 'some value to send';
  }
  stream.respondWithFile('/some/file',
                         { 'content-type': 'text/plain' },
                         { getTrailers });
});
```

*Note*: The HTTP/1 specification forbids trailers from containing HTTP/2
"pseudo-header" fields (e.g. `':status'`, `':path'`, etc). An `'error'` event
will be emitted if the `getTrailers` callback attempts to set such header
fields.

