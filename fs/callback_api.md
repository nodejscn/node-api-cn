
The callback APIs perform all operations asynchronously, without blocking the
event loop, then invoke a callback function upon completion or error.

The callback APIs use the underlying Node.js threadpool to perform file
system operations off the event loop thread. These operations are not
synchronized or threadsafe. Care must be taken when performing multiple
concurrent modifications on the same file or data corruption may occur.

