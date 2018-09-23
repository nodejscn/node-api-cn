<!-- YAML
added: v0.3.6
changes:
  - version: v10.9.0
    pr-url: https://github.com/nodejs/node/pull/21616
    description: allow both url and options to be passed to `http.request()`
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10638
    description: The `options` parameter can be a WHATWG `URL` object.
-->

* `url` {string | URL}
* `options` {Object}
  * `protocol` {string} Protocol to use. **Default:** `'http:'`.
  * `host` {string} A domain name or IP address of the server to issue the
    request to. **Default:** `'localhost'`.
  * `hostname` {string} Alias for `host`. To support [`url.parse()`][],
    `hostname` is preferred over `host`.
  * `family` {number} IP address family to use when resolving `host` and
    `hostname`. Valid values are `4` or `6`. When unspecified, both IP v4 and
    v6 will be used.
  * `port` {number} Port of remote server. **Default:** `80`.
  * `localAddress` {string} Local interface to bind for network connections.
  * `socketPath` {string} Unix Domain Socket (use one of `host:port` or
    `socketPath`).
  * `method` {string} A string specifying the HTTP request method. **Default:**
    `'GET'`.
  * `path` {string} Request path. Should include query string if any.
    E.G. `'/index.html?page=12'`. An exception is thrown when the request path
    contains illegal characters. Currently, only spaces are rejected but that
    may change in the future. **Default:** `'/'`.
  * `headers` {Object} An object containing request headers.
  * `auth` {string} Basic authentication i.e. `'user:password'` to compute an
    Authorization header.
  * `agent` {http.Agent | boolean} Controls [`Agent`][] behavior. Possible
    values:
    * `undefined` (default): use [`http.globalAgent`][] for this host and port.
    * `Agent` object: explicitly use the passed in `Agent`.
    * `false`: causes a new `Agent` with default values to be used.
  * `createConnection` {Function} A function that produces a socket/stream to
    use for the request when the `agent` option is not used. This can be used to
    avoid creating a custom `Agent` class just to override the default
    `createConnection` function. See [`agent.createConnection()`][] for more
    details. Any [`Duplex`][] stream is a valid return value.
  * `timeout` {number}: A number specifying the socket timeout in milliseconds.
    This will set the timeout before the socket is connected.
  * `setHost` {boolean}: Specifies whether or not to automatically add the
    `Host` header. Defaults to `true`.
* `callback` {Function}
* Returns: {http.ClientRequest}

Node.js maintains several connections per server to make HTTP requests.
This function allows one to transparently issue requests.

`url` can be a string or a [`URL`][] object. If `url` is a
string, it is automatically parsed with [`url.parse()`][]. If it is a [`URL`][]
object, it will be automatically converted to an ordinary `options` object.

If both `url` and `options` are specified, the objects are merged, with the
`options` properties taking precedence.

The optional `callback` parameter will be added as a one-time listener for
the [`'response'`][] event.

`http.request()` returns an instance of the [`http.ClientRequest`][]
class. The `ClientRequest` instance is a writable stream. If one needs to
upload a file with a POST request, then write to the `ClientRequest` object.

```js
const postData = querystring.stringify({
  'msg': 'Hello World!'
});

const options = {
  hostname: 'www.google.com',
  port: 80,
  path: '/upload',
  method: 'POST',
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Content-Length': Buffer.byteLength(postData)
  }
};

const req = http.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`);
  console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`BODY: ${chunk}`);
  });
  res.on('end', () => {
    console.log('No more data in response.');
  });
});

req.on('error', (e) => {
  console.error(`problem with request: ${e.message}`);
});

// write data to request body
req.write(postData);
req.end();
```

Note that in the example `req.end()` was called. With `http.request()` one
must always call `req.end()` to signify the end of the request -
even if there is no data being written to the request body.

If any error is encountered during the request (be that with DNS resolution,
TCP level errors, or actual HTTP parse errors) an `'error'` event is emitted
on the returned request object. As with all `'error'` events, if no listeners
are registered the error will be thrown.

There are a few special headers that should be noted.

* Sending a 'Connection: keep-alive' will notify Node.js that the connection to
  the server should be persisted until the next request.

* Sending a 'Content-Length' header will disable the default chunked encoding.

* Sending an 'Expect' header will immediately send the request headers.
  Usually, when sending 'Expect: 100-continue', both a timeout and a listener
  for the `'continue'` event should be set. See RFC2616 Section 8.2.3 for more
  information.

* Sending an Authorization header will override using the `auth` option
  to compute basic authentication.

Example using a [`URL`][] as `options`:

```js
const options = new URL('http://abc:xyz@example.com');

const req = http.request(options, (res) => {
  // ...
});
```

In a successful request, the following events will be emitted in the following
order:

* `'socket'`
* `'response'`
  * `'data'` any number of times, on the `res` object
    (`'data'` will not be emitted at all if the response body is empty, for
    instance, in most redirects)
  * `'end'` on the `res` object
* `'close'`

In the case of a connection error, the following events will be emitted:

* `'socket'`
* `'error'`
* `'close'`

If `req.abort()` is called before the connection succeeds, the following events
will be emitted in the following order:

* `'socket'`
* (`req.abort()` called here)
* `'abort'`
* `'close'`
* `'error'` with an error with message `'Error: socket hang up'` and code
  `'ECONNRESET'`

If `req.abort()` is called after the response is received, the following events
will be emitted in the following order:

* `'socket'`
* `'response'`
  * `'data'` any number of times, on the `res` object
* (`req.abort()` called here)
* `'abort'`
* `'close'`
  * `'aborted'` on the `res` object
  * `'end'` on the `res` object
  * `'close'` on the `res` object

Note that setting the `timeout` option or using the `setTimeout()` function will
not abort the request or do anything besides add a `'timeout'` event.

















































