
`SystemError` instances may have an additional `info` property whose
value is an object with additional details about the error conditions.

The following properties are provided:

* `code` {string} The string error code
* `errno` {number} The system-provided error number
* `message` {string} A system-provided human readable description of the error
* `syscall` {string} The name of the system call that triggered the error
* `path` {Buffer} When reporting a file system error, the `path` will identify
  the file path.
* `dest` {Buffer} When reporting a file system error, the `dest` will identify
  the file path destination (if any).

