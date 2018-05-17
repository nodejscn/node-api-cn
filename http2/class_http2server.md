<!-- YAML
added: v8.4.0
-->

* Extends: {net.Server}

In `Http2Server`, there are no `'clientError'` events as there are in
HTTP1. However, there are `'sessionError'`, and `'streamError'` events for
errors emitted on the socket, or from `Http2Session` or `Http2Stream` instances.

