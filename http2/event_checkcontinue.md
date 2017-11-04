<!-- YAML
added: v8.5.0
-->

* `request` {http2.Http2ServerRequest}
* `response` {http2.Http2ServerResponse}

If a [`'request'`][] listener is registered or [`http2.createServer()`][] is
supplied a callback function, the `'checkContinue'` event is emitted each time
a request with an HTTP `Expect: 100-continue` is received. If this event is
not listened for, the server will automatically respond with a status
`100 Continue` as appropriate.

Handling this event involves calling [`response.writeContinue()`][] if the client
should continue to send the request body, or generating an appropriate HTTP
response (e.g. 400 Bad Request) if the client should not continue to send the
request body.

Note that when this event is emitted and handled, the [`'request'`][] event will
not be emitted.

