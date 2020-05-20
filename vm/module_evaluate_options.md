
* `options` {Object}
  * `timeout` {integer} Specifies the number of milliseconds to evaluate
    before terminating execution. If execution is interrupted, an [`Error`][]
    will be thrown. This value must be a strictly positive integer.
  * `breakOnSigint` {boolean} If `true`, the execution will be terminated when
    `SIGINT` (Ctrl+C) is received. Existing handlers for the event that have
    been attached via `process.on('SIGINT')` will be disabled during script
    execution, but will continue to work after that. If execution is
    interrupted, an [`Error`][] will be thrown. **Default:** `false`.
* Returns: {Promise}

Evaluate the module.

This must be called after the module has been linked; otherwise it will reject.
It could be called also when the module has already been evaluated, in which
case it will either do nothing if the initial evaluation ended in success
(`module.status` is `'evaluated'`) or it will re-throw the exception that the
initial evaluation resulted in (`module.status` is `'errored'`).

This method cannot be called while the module is being evaluated
(`module.status` is `'evaluating'`).

Corresponds to the [Evaluate() concrete method][] field of [Cyclic Module
Record][]s in the ECMAScript specification.

