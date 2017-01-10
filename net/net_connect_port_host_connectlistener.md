<!-- YAML
added: v0.1.90
-->

A factory function, which returns a new [`net.Socket`][] and automatically
connects to the supplied `port` and `host`.

If `host` is omitted, `'localhost'` will be assumed.

The `connectListener` parameter will be added as a listener for the
[`'connect'`][] event once.

