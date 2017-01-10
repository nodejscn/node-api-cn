<!-- YAML
added: v0.1.90
-->

* `path` {String}
* `backlog` {Number}
* `callback` {Function}

Start a local socket server listening for connections on the given `path`.

This function is asynchronous.  When the server has been bound,
[`'listening'`][] event will be emitted.  The last parameter `callback`
will be added as a listener for the [`'listening'`][] event.

On UNIX, the local domain is usually known as the UNIX domain. The path is a
filesystem path name. It gets truncated to `sizeof(sockaddr_un.sun_path)`
bytes, decreased by 1. It varies on different operating system between 91 and
107 bytes. The typical values are 107 on Linux and 103 on OS X. The path is
subject to the same naming conventions and permissions checks as would be done
on file creation, will be visible in the filesystem, and will *persist until
unlinked*.

On Windows, the local domain is implemented using a named pipe. The path *must*
refer to an entry in `\\?\pipe\` or `\\.\pipe\`. Any characters are permitted,
but the latter may do some processing of pipe names, such as resolving `..`
sequences. Despite appearances, the pipe name space is flat.  Pipes will *not
persist*, they are removed when the last reference to them is closed. Do not
forget JavaScript string escaping requires paths to be specified with
double-backslashes, such as:

```js
net.createServer().listen(
    path.join('\\\\?\\pipe', process.cwd(), 'myctl'))
```

The parameter `backlog` behaves the same as in
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`].

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

