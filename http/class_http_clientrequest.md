<!-- YAML
added: v0.1.17
-->

This object is created internally and returned from [`http.request()`][].  It
represents an _in-progress_ request whose header has already been queued.  The
header is still mutable using the `setHeader(name, value)`, `getHeader(name)`,
`removeHeader(name)` API.  The actual header will be sent along with the first
data chunk or when closing the connection.

To get the response, add a listener for [`'response'`][] to the request object.
[`'response'`][] will be emitted from the request object when the response
headers have been received.  The [`'response'`][] event is executed with one
argument which is an instance of [`http.IncomingMessage`][].

During the [`'response'`][] event, one can add listeners to the
response object; particularly to listen for the `'data'` event.

If no [`'response'`][] handler is added, then the response will be
entirely discarded.  However, if you add a [`'response'`][] event handler,
then you **must** consume the data from the response object, either by
calling `response.read()` whenever there is a `'readable'` event, or
by adding a `'data'` handler, or by calling the `.resume()` method.
Until the data is consumed, the `'end'` event will not fire.  Also, until
the data is read it will consume memory that can eventually lead to a
'process out of memory' error.

Note: Node.js does not check whether Content-Length and the length of the body
which has been transmitted are equal or not.

The request implements the [Writable Stream][] interface. This is an
[`EventEmitter`][] with the following events:

