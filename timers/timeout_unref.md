<!-- YAML
added: v0.9.1
-->

When called, the active `Timeout` object will not require the Node.js event loop
to remain active. If there is no other activity keeping the event loop running,
the process may exit before the `Timeout` object's callback is invoked. Calling
`timeout.unref()` multiple times will have no effect.

*Note*: Calling `timeout.unref()` creates an internal timer that will wake the
Node.js event loop. Creating too many of these can adversely impact performance
of the Node.js application.

Returns a reference to the `Timeout`.

