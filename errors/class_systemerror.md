
* Extends: {errors.Error}

Node.js generates system errors when exceptions occur within its runtime
environment. These usually occur when an application violates an operating
system constraint. For example, a system error will occur if an application
attempts to read a file that does not exist.

* `address` {string} If present, the address to which a network connection
  failed
* `code` {string} The string error code
* `dest` {string} If present, the file path destination when reporting a file
  system error
* `errno` {number} The system-provided error number
* `info` {Object} If present, extra details about the error condition
* `message` {string} A system-provided human-readable description of the error
* `path` {string} If present, the file path when reporting a file system error
* `port` {number} If present, the network connection port that is not available
* `syscall` {string} The name of the system call that triggered the error

