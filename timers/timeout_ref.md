<!-- YAML
added: v0.9.1
-->

When called, requests that the Node.js event loop *not* exit so long as the
`Timeout` is active. Calling `timeout.ref()` multiple times will have no effect.

*Note*: By default, all `Timeout` objects are "ref'd", making it normally
unnecessary to call `timeout.ref()` unless `timeout.unref()` had been called
previously.

Returns a reference to the `Timeout`.

