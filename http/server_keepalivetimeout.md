<!-- YAML
added: v8.0.0
-->

* {number} Timeout in milliseconds. Defaults to 5000 (5 seconds).

The number of milliseconds of inactivity a server needs to wait for additional
incoming data, after it has finished writing the last response, before a socket
will be destroyed. If the server receives new data before the keep-alive
timeout has fired, it will reset the regular inactivity timeout, i.e.,
[`server.timeout`][].

A value of 0 will disable the keep-alive timeout behavior on incoming connections.

*Note*: The socket timeout logic is set up on connection, so changing this
value only affects new connections to the server, not any existing connections.

