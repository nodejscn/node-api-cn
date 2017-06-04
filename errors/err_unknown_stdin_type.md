
An error using the `'ERR_UNKNOWN_STDIN_TYPE'` code is thrown specifically when
an attempt is made to launch a Node.js process with an unknown `stdin` file
type. Errors of this kind cannot *typically* be caused by errors in user code,
although it is not impossible. Occurrences of this error are most likely an
indication of a bug within Node.js itself.

<a id="ERR_UNKNOWN_STREAM_TYPE"></a>
