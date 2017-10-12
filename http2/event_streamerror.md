<!-- YAML
added: v8.5.0
-->

* `socket` {http2.ServerHttp2Stream}

If an `ServerHttp2Stream` emits an `'error'` event, it will be forwarded here.
The stream will already be destroyed when this event is triggered.

