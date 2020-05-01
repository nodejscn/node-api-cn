<!-- YAML
added: v0.0.1
deprecated:
 - v13.4.0
 - v12.16.0
-->

> Stability: 0 - Deprecated. Use [`request.writableEnded`][].

* {boolean}

The `request.finished` property will be `true` if [`request.end()`][]
has been called. `request.end()` will automatically be called if the
request was initiated via [`http.get()`][].

