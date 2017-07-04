
Initiate a connection on a given socket.

Possible signatures:

* [socket.connect(options[, connectListener])][`socket.connect(options)`]
* [socket.connect(path[, connectListener])][`socket.connect(path)`]
  for [IPC][] connections.
* [socket.connect(port[, host][, connectListener])][`socket.connect(port, host)`]
  for TCP connections.
* Returns: {net.Socket} The socket itself.

This function is asynchronous. When the connection is established, the
[`'connect'`][] event will be emitted. If there is a problem connecting,
instead of a [`'connect'`][] event, an [`'error'`][] event will be emitted with
the error passed to the [`'error'`][] listener.
The last parameter `connectListener`, if supplied, will be added as a listener
for the [`'connect'`][] event **once**.

