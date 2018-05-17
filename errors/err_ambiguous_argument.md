
This is triggered by the `assert` module in case e.g.,
`assert.throws(fn, message)` is used in a way that the message is the thrown
error message. This is ambiguous because the message is not verifying the error
message and will only be thrown in case no error is thrown.

<a id="ERR_ARG_NOT_ITERABLE"></a>
