<!-- YAML
added: v8.4.0
-->

* `session` {Http2Session}
* `socket` {net.Socket}

The `'connect'` event is emitted once the `Http2Session` has been successfully
connected to the remote peer and communication may begin.

User code will typically not listen for this event directly.

