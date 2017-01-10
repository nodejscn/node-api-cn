<!-- YAML
added: v0.1.90
-->

A factory function, which returns a new unix [`net.Socket`][] and automatically
connects to the supplied `path`.

The `connectListener` parameter will be added as a listener for the
[`'connect'`][] event once.

