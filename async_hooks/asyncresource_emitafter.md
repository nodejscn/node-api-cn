
* Returns {undefined}

Call all `after` callbacks. If nested calls to `emitBefore()` were made, then
make sure the stack is unwound properly. Otherwise an error will be thrown.

If the user's callback throws an exception then `emitAfter()` will
automatically be called for all `asyncId`s on the stack if the error is handled by
a domain or `'uncaughtException'` handler.

