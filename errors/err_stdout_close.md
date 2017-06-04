
An error using the `'ERR_STDOUT_CLOSE'` code is thrown specifically when an
attempt is made to close the `process.stdout` stream. By design, Node.js does
not allow `stdout` or `stderr` Streams to be closed by user code.

<a id="ERR_UNKNOWN_BUILTIN_MODULE"></a>
