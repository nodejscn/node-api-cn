
[`net.connect()`][], [`net.createConnection()`][], [`server.listen()`][] and
[`socket.connect()`][] take a `path` parameter to identify IPC endpoints.

On UNIX, the local domain is also known as the UNIX domain. The path is a
filesystem path name. It gets truncated to `sizeof(sockaddr_un.sun_path) - 1`,
which varies on different operating system between 91 and 107 bytes.
The typical values are 107 on Linux and 103 on macOS. The path is
subject to the same naming conventions and permissions checks as would be done
on file creation. It will be visible in the filesystem, and will *persist until
unlinked*.

On Windows, the local domain is implemented using a named pipe. The path *must*
refer to an entry in `\\?\pipe\` or `\\.\pipe\`. Any characters are permitted,
but the latter may do some processing of pipe names, such as resolving `..`
sequences. Despite appearances, the pipe name space is flat. Pipes will *not
persist*, they are removed when the last reference to them is closed. Do not
forget JavaScript string escaping requires paths to be specified with
double-backslashes, such as:

```js
net.createServer().listen(
  path.join('\\\\?\\pipe', process.cwd(), 'myctl'));
```

