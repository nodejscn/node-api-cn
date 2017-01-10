<!-- YAML
added: v0.5.8
-->

The `tty.ReadStream` class is a subclass of `net.Socket` that represents the
readable side of a TTY. In normal circumstances `process.stdin` will be the
only `tty.ReadStream` instance in a Node.js process and there should be no
reason to create additional instances.

