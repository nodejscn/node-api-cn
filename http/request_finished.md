<!-- YAML
added: v0.0.1
deprecated: v12.16.0
-->

> Stability: 0 - Deprecated. Use [`request.writableEnded`][].

* {boolean}

如果调用了 [`request.end()`]，则 `request.finished` 属性将为 `true`。 
如果请求是通过 [`http.get()`] 发起的，则会自动调用 `request.end()`。


