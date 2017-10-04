<!-- YAML
added: v8.4.0
-->

* Extends: {net.Server}

In `Http2Server`, there is no `'clientError'` event as there is in
HTTP1. However, there are `'socketError'`, `'sessionError'`,  and
`'streamError'`, for error happened on the socket, session or stream
respectively.

