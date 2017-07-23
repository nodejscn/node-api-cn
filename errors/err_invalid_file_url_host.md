
Used when a Node.js API that consumes `file:` URLs (such as certain functions in
the [`fs`][] module) encounters a file URL with an incompatible host. Currently,
this situation can only occur on Unix-like systems, where only `localhost` or an
empty host is supported.

<a id="ERR_INVALID_FILE_URL_PATH"></a>
