<!-- YAML
added: v0.1.99
-->

The `'close'` event is emitted after a socket is closed with [`close()`][].
Once triggered, no new `'message'` events will be emitted on this socket.
`'close'`事件将在使用[`close()`][]关闭一个 socket 之后触发。该事件一旦触发，这个 socket 上将不会触发新的`'message'`事件。

