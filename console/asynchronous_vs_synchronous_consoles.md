
The console functions are usually asynchronous unless the destination is a file.
Disks are fast and operating systems normally employ write-back caching;
it should be a very rare occurrence indeed that a write blocks, but it
is possible.

Additionally, console functions are blocking when outputting to TTYs
(terminals) on OS X as a workaround for the OS's very small, 1kb buffer size.
This is to prevent interleaving between `stdout` and `stderr`.

