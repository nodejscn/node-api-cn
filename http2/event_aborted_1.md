<!-- YAML
added: v8.4.0
-->

The `'aborted'` event is emitted whenever a `Http2ServerRequest` instance is
abnormally aborted in mid-communication.

*Note*: The `'aborted'` event will only be emitted if the
`Http2ServerRequest` writable side has not been ended.

