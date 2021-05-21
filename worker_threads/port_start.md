<!-- YAML
added: v10.5.0
-->

Starts receiving messages on this `MessagePort`. When using this port
as an event emitter, this is called automatically once `'message'`
listeners are attached.

This method exists for parity with the Web `MessagePort` API. In Node.js,
it is only useful for ignoring messages when no event listener is present.
Node.js also diverges in its handling of `.onmessage`. Setting it
automatically calls `.start()`, but unsetting it lets messages queue up
until a new handler is set or the port is discarded.

