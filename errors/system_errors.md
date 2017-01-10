
System errors are generated when exceptions occur within the program's
runtime environment. Typically, these are operational errors that occur
when an application violates an operating system constraint such as attempting
to read a file that does not exist or when the user does not have sufficient
permissions.

System errors are typically generated at the syscall level: an exhaustive list
of error codes and their meanings is available by running `man 2 intro` or
`man 3 errno` on most Unices; or [online][].

In Node.js, system errors are represented as augmented `Error` objects with
added properties.

