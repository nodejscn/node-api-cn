<!-- YAML
added: v5.5.0
-->

* `request` {http.ClientRequest}
* `response` {http.ServerResponse}

Emitted each time a request with an HTTP `Expect` header is received, where the
value is not `100-continue`. If this event isn't listened for, the server will
automatically respond with a `417 Expectation Failed` as appropriate.

Note that when this event is emitted and handled, the [`'request'`][] event will
not be emitted.

