<!-- YAML
added: v0.3.0
-->

* `request` {http.IncomingMessage}
* `response` {http.ServerResponse}

Emitted each time a request with an HTTP `Expect: 100-continue` is received.
If this event isn't listened for, the server will automatically respond
with a `100 Continue` as appropriate.

Handling this event involves calling [`response.writeContinue()`][] if the client
should continue to send the request body, or generating an appropriate HTTP
response (e.g. 400 Bad Request) if the client should not continue to send the
request body.

Note that when this event is emitted and handled, the [`'request'`][] event will
not be emitted.

