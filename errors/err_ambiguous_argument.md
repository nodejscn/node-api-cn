
A function argument is being used in a way that suggests that the function
signature may be misunderstood. This is thrown by the `assert` module when the
`message` parameter in `assert.throws(block, message)` matches the error message
thrown by `block` because that usage suggests that the user believes `message`
is the expected message rather than the message the `AssertionError` will
display if `block` does not throw.

<a id="ERR_ARG_NOT_ITERABLE"></a>
