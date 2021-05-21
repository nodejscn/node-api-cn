<!-- YAML
added: v0.9.12
-->

* `msesc` {number}
* `callback` {Function} Optional function to be called when a timeout
occurs, Same as binding to the `timeout` event.
* Returns: {this}

Once a socket is associated with the message and is connected,
[`socket.setTimeout()`][] will be called with `msecs` as the first parameter.

