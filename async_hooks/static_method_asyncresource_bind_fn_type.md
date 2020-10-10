<!-- YAML
added: v14.8.0
-->

* `fn` {Function} The function to bind to the current execution context.
* `type` {string} An optional name to associate with the underlying
  `AsyncResource`.

Binds the given function to the current execution context.

The returned function will have an `asyncResource` property referencing
the `AsyncResource` to which the function is bound.

