<!-- YAML
added: v8.4.0
-->

The `'socketError'` event is emitted when an `'error'` is emitted on the
`Socket` instance bound to the `Http2Session`. If this event is not handled,
the `'error'` event will be re-emitted on the `Socket`.

For `ServerHttp2Session` instances, a `'socketError'` event listener is always
registered that will, by default, forward the event on to the owning
`Http2Server` instance if no additional handlers are registered.

