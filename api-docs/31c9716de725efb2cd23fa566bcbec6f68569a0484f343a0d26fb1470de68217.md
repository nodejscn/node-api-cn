<!-- YAML
added: v10.5.0
-->

* `callback` {Function}
  * `err` {Error}
  * `exitCode` {integer}

Stop all JavaScript execution in the worker thread as soon as possible.
`callback` is an optional function that is invoked once this operation is known
to have completed.

**Warning**: Currently, not all code in the internals of Node.js is prepared to
expect termination at arbitrary points in time and may crash if it encounters
that condition. Consequently, only call `.terminate()` if it is known that the
Worker thread is not accessing Node.js core modules other than what is exposed
in the `worker` module.

