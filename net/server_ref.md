<!-- YAML
added: v0.9.1
-->

* Returns: {net.Server}

Opposite of `unref`, calling `ref` on a previously `unref`d server will *not*
let the program exit if it's the only server left (the default behavior). If
the server is `ref`d calling `ref` again will have no effect.

