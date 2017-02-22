
* `callback` {Function} The callback function
* Returns: {Function} The intercepted function

This method is almost identical to [`domain.bind(callback)`][].  However, in
addition to catching thrown errors, it will also intercept [`Error`][]
objects sent as the first argument to the function.

In this way, the common `if (err) return callback(err);` pattern can be replaced
with a single error handler in a single place.

