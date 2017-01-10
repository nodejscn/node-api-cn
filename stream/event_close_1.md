<!-- YAML
added: v0.9.4
-->

The `'close'` event is emitted when the stream and any of its underlying
resources (a file descriptor, for example) have been closed. The event indicates
that no more events will be emitted, and no further computation will occur.

Not all [Readable][] streams will emit the `'close'` event.

