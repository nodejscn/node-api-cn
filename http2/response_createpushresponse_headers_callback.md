<!-- YAML
added: v8.4.0
-->

* `headers` {HTTP/2 Headers Object} An object describing the headers
* `callback` {Function} Called once `http2stream.pushStream()` is finished,
  or either when the attempt to create the pushed `Http2Stream` has failed or
  has been rejected, or the state of `Http2ServerRequest` is closed prior to
  calling the `http2stream.pushStream()` method
  * `err` {Error}
  * `res` {http2.Http2ServerResponse} The newly-created `Http2ServerResponse`
    object

Call [`http2stream.pushStream()`][] with the given headers, and wrap the
given [`Http2Stream`][] on a newly created `Http2ServerResponse` as the callback
parameter if successful. When `Http2ServerRequest` is closed, the callback is
called with an error `ERR_HTTP2_INVALID_STREAM`.

