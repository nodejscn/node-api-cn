<!-- YAML
added: v8.4.0
-->

* {boolean}

Indicates whether the `Http2Session` is currently waiting for acknowledgment of
a sent `SETTINGS` frame. Will be `true` after calling the
`http2session.settings()` method. Will be `false` once all sent `SETTINGS`
frames have been acknowledged.

