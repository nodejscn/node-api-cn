<!-- YAML
added: v0.7.0
-->

* `request` {http.IncomingMessage} Arguments for the HTTP request, as it is in
  the [`'request'`][] event
* `socket` {net.Socket} Network socket between the server and client
* `head` {Buffer} The first packet of the tunneling stream (may be empty)

Emitted each time a client requests an HTTP `CONNECT` method. If this event isn't
listened for, then clients requesting a `CONNECT` method will have their
connections closed.

After this event is emitted, the request's socket will not have a `'data'`
event listener, meaning you will need to bind to it in order to handle data
sent to the server on that socket.

