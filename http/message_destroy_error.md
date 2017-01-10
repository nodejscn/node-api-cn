<!-- YAML
added: v0.3.0
-->

* `error` {Error}

Calls `destroy()` on the socket that received the `IncomingMessage`. If `error`
is provided, an `'error'` event is emitted and `error` is passed as an argument
to any listeners on the event.

