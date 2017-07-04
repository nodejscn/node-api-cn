<!-- YAML
added: v0.9.1
-->

* Returns: {net.Socket} The socket itself.

Opposite of `unref`, calling `ref` on a previously `unref`d socket will *not*
let the program exit if it's the only socket left (the default behavior). If
the socket is `ref`d calling `ref` again will have no effect.

