
This list is **not exhaustive**, but enumerates many of the common system
errors encountered when writing a Node.js program. An exhaustive list may be
found [here][online].

- `EACCES` (Permission denied): An attempt was made to access a file in a way
  forbidden by its file access permissions.

- `EADDRINUSE` (Address already in use):  An attempt to bind a server
  ([`net`][], [`http`][], or [`https`][]) to a local address failed due to
  another server on the local system already occupying that address.

- `ECONNREFUSED` (Connection refused): No connection could be made because the
  target machine actively refused it. This usually results from trying to
  connect to a service that is inactive on the foreign host.

- `ECONNRESET` (Connection reset by peer): A connection was forcibly closed by
  a peer. This normally results from a loss of the connection on the remote
  socket due to a timeout or reboot. Commonly encountered via the [`http`][]
  and [`net`][] modules.

- `EEXIST` (File exists): An existing file was the target of an operation that
  required that the target not exist.

- `EISDIR` (Is a directory): An operation expected a file, but the given
  pathname was a directory.

- `EMFILE` (Too many open files in system): Maximum number of
  [file descriptors][] allowable on the system has been reached, and
  requests for another descriptor cannot be fulfilled until at least one
  has been closed. This is encountered when opening many files at once in
  parallel, especially on systems (in particular, OS X) where there is a low
  file descriptor limit for processes. To remedy a low limit, run
  `ulimit -n 2048` in the same shell that will run the Node.js process.

- `ENOENT` (No such file or directory): Commonly raised by [`fs`][] operations
  to indicate that a component of the specified pathname does not exist -- no
  entity (file or directory) could be found by the given path.

- `ENOTDIR` (Not a directory): A component of the given pathname existed, but
  was not a directory as expected. Commonly raised by [`fs.readdir`][].

- `ENOTEMPTY` (Directory not empty): A directory with entries was the target
  of an operation that requires an empty directory -- usually [`fs.unlink`][].

- `EPERM` (Operation not permitted): An attempt was made to perform an
  operation that requires elevated privileges.

- `EPIPE` (Broken pipe): A write on a pipe, socket, or FIFO for which there is
  no process to read the data. Commonly encountered at the [`net`][] and
  [`http`][] layers, indicative that the remote side of the stream being
  written to has been closed.

- `ETIMEDOUT` (Operation timed out): A connect or send request failed because
  the connected party did not properly respond after a period of time. Usually
  encountered by [`http`][] or [`net`][] -- often a sign that a `socket.end()`
  was not properly called.

[`fs.readdir`]: fs.html#fs_fs_readdir_path_options_callback
[`fs.readFileSync`]: fs.html#fs_fs_readfilesync_file_options
[`fs.unlink`]: fs.html#fs_fs_unlink_path_callback
[`fs`]: fs.html
[`http`]: http.html
[`https`]: https.html
[`net`]: net.html
[`process.on('uncaughtException')`]: process.html#process_event_uncaughtexception
[domains]: domain.html
[event emitter-based]: events.html#events_class_eventemitter
[file descriptors]: https://en.wikipedia.org/wiki/File_descriptor
[online]: http://man7.org/linux/man-pages/man3/errno.3.html
[stream-based]: stream.html
[syscall]: http://man7.org/linux/man-pages/man2/syscall.2.html
[try-catch]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch
[V8's stack trace API]: https://github.com/v8/v8/wiki/Stack-Trace-API
[vm]: vm.html
