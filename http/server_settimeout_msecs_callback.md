<!-- YAML
added: v0.9.12
-->

* `msecs` {Number}
* `callback` {Function}

Sets the timeout value for sockets, and emits a `'timeout'` event on
the Server object, passing the socket as an argument, if a timeout
occurs.

If there is a `'timeout'` event listener on the Server object, then it
will be called with the timed-out socket as an argument.

By default, the Server's timeout value is 2 minutes, and sockets are
destroyed automatically if they time out.  However, if you assign a
callback to the Server's `'timeout'` event, then you are responsible
for handling socket timeouts.

Returns `server`.

