<!-- YAML
added: v0.3.4
-->

Creates a new socket object.

* `options` {Object} Available options are:
  * `fd`: {number} If specified, wrap around an existing socket with
    the given file descriptor, otherwise a new socket will be created.
  * `allowHalfOpen` {boolean} Indicates whether half-opened TCP connections
    are allowed. See [`net.createServer()`][] and the [`'end'`][] event
    for details. Defaults to `false`.
  * `readable` {boolean} Allow reads on the socket when an `fd` is passed,
    otherwise ignored. Defaults to `false`.
  * `writable` {boolean} Allow writes on the socket when an `fd` is passed,
    otherwise ignored. Defaults to `false`.
* Returns: {net.Socket}

The newly created socket can be either a TCP socket or a streaming [IPC][]
endpoint, depending on what it [`connect()`][`socket.connect()`] to.

