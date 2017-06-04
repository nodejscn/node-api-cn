
An error using the `'ERR_STDERR_CLOSE'` code is thrown specifically when an
attempt is made to close the `process.stderr` stream. By design, Node.js does
not allow `stdout` or `stderr` Streams to be closed by user code.

<a id="ERR_STDOUT_CLOSE"></a>
