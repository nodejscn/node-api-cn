<!-- YAML
added: v0.9.1
-->

* Returns: {net.Socket} The socket itself.

Calling `unref` on a socket will allow the program to exit if this is the only
active socket in the event system. If the socket is already `unref`d calling
`unref` again will have no effect.

