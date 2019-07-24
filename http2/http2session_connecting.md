<!-- YAML
added: v10.0.0
-->

* {boolean}

Will be `true` if this `Http2Session` instance is still connecting, will be set
to `false` before emitting `connect` event and/or calling the `http2.connect`
callback.

