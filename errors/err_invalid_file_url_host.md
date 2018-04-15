
A Node.js API that consumes `file:` URLs (such as certain functions in the
[`fs`][] module) encountered a file URL with an incompatible host. This
situation can only occur on Unix-like systems where only `localhost` or an empty
host is supported.

<a id="ERR_INVALID_FILE_URL_PATH"></a>