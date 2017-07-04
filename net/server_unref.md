<!-- YAML
added: v0.9.1
-->

* Returns: {net.Server}

Calling `unref` on a server will allow the program to exit if this is the only
active server in the event system. If the server is already `unref`d calling
`unref` again will have no effect.

