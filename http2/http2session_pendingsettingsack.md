<!-- YAML
added: v8.4.0
-->

* Value: {boolean}

Indicates whether or not the `Http2Session` is currently waiting for an
acknowledgement for a sent SETTINGS frame. Will be `true` after calling the
`http2session.settings()` method. Will be `false` once all sent SETTINGS
frames have been acknowledged.

