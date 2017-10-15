
* Returns: {undefined}

Call all `before` callbacks to notify that a new asynchronous execution context
is being entered. If nested calls to `emitBefore()` are made, the stack of
`asyncId`s will be tracked and properly unwound.

