<!-- YAML
added: v0.9.12
-->

* `msecs` {Number}
* `callback` {Function}

Sets the Socket's timeout value to `msecs`.  If a callback is
provided, then it is added as a listener on the `'timeout'` event on
the response object.

If no `'timeout'` listener is added to the request, the response, or
the server, then sockets are destroyed when they time out.  If you
assign a handler on the request, the response, or the server's
`'timeout'` events, then it is your responsibility to handle timed out
sockets.

Returns `response`.

