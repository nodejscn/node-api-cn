<!-- YAML
added: v8.4.0
deprecated: v13.4.0
-->

> Stability: 0 - Deprecated. Use [`response.writableEnded`][].

* {boolean}

Boolean value that indicates whether the response has completed. Starts
as `false`. After [`response.end()`][] executes, the value will be `true`.

