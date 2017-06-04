
An error with the `'ERR_INVALID_FILE_URL_PATH'` code may be thrown when a
Node.js API that consumes `file:` URLs (such as certain functions in the
[`fs`][] module) encounters a file URL with an incompatible path. The exact
semantics for determining whether a path can be used is platform-dependent.

<a id="ERR_INVALID_HANDLE_TYPE"></a>
