<!-- YAML
added: v0.5.9
-->

* `timeout` {Number} Milliseconds before a request is considered to be timed out.
* `callback` {Function} Optional function to be called when a timeout occurs. Same as binding to the `timeout` event.

Once a socket is assigned to this request and is connected
[`socket.setTimeout()`][] will be called.

Returns `request`.

