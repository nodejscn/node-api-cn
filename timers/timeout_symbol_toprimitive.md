<!-- YAML
added: v14.9.0
-->

* Returns: {integer} a number that can be used to reference this `timeout`

Coerce a `Timeout` to a primitive. The primitive can be used to
clear the `Timeout`. The primitive can only be used in the
same thread where the timeout was created. Therefore, to use it
across [`worker_threads`][] it must first be passed to the correct
thread. This allows enhanced compatibility with browser
`setTimeout()` and `setInterval()` implementations.

