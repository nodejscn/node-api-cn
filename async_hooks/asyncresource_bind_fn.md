<!-- YAML
added: v14.8.0
-->

* `fn` {Function} The function to bind to the current `AsyncResource`.

Binds the given function to execute to this `AsyncResource`'s scope.

The returned function will have an `asyncResource` property referencing
the `AsyncResource` to which the function is bound.

