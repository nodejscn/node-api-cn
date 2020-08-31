<!-- YAML
added: v14.9.0
-->

* Returns: {integer} number that can be used to reference this `timeout`

Coerce a `Timeout` to a primitive, a primitive will be generated that
can be used to clear the `Timeout`.
The generated number can only be used in the same thread where timeout
was created. Therefore to use it cross [`worker_threads`][] it has
to first be passed to a correct thread.
This allows enhanced compatibility with browser's `setTimeout()`, and
`setInterval()` implementations.

