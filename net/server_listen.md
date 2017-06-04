
Start a server listening for connections. A `net.Server` can be a TCP or
a [IPC][] server depending on what it listens to.

Possible signatures:

* [`server.listen(handle[, backlog][, callback])`][`server.listen(handle)`]
* [`server.listen(options[, callback])`][`server.listen(options)`]
* [`server.listen(path[, backlog][, callback])`][`server.listen(path)`]
  for [IPC][] servers
* [`server.listen([port][, host][, backlog][, callback])`][`server.listen(port, host)`]
  for TCP servers

This function is asynchronous.  When the server starts listening, the
[`'listening'`][] event will be emitted.  The last parameter `callback`
will be added as a listener for the [`'listening'`][] event.

All `listen()` methods can take a `backlog` parameter to specify the maximum
length of the queue of pending connections. The actual length will be determined
by the OS through sysctl settings such as `tcp_max_syn_backlog` and `somaxconn`
on Linux. The default value of this parameter is 511 (not 512).


*Note*:

* All [`net.Socket`][] are set to `SO_REUSEADDR` (See [socket(7)][] for
  details).

* The `server.listen()` method may be called multiple times. Each
  subsequent call will *re-open* the server using the provided options.

One of the most common errors raised when listening is `EADDRINUSE`.
This happens when another server is already listening on the requested
`port` / `path` / `handle`. One way to handle this would be to retry
after a certain amount of time:

```js
server.on('error', (e) => {
  if (e.code === 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(() => {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});
```

