<!-- YAML
added: v8.4.0
-->

The `'aborted'` event is emitted whenever a `Http2Stream` instance is
abnormally aborted in mid-communication.
Its listener does not expect any arguments.

The `'aborted'` event will only be emitted if the `Http2Stream` writable side
has not been ended.

