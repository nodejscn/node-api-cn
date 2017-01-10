<!-- YAML
added: v0.5.8
-->

The `tty.WriteStream` class is a subclass of `net.Socket` that represents the
writable side of a TTY. In normal circumstances, `process.stdout` and
`process.stderr` will be the only `tty.WriteStream` instances created for a
Node.js process and there should be no reason to create additional instances.

