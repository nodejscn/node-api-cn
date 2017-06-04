<!-- YAML
added: v0.1.90
-->

Begin accepting connections on the specified `port` and `hostname`. If the
`hostname` is omitted, the server will accept connections on any IPv6 address
(`::`) when IPv6 is available, or any IPv4 address (`0.0.0.0`) otherwise.
Omit the port argument, or use a port value of `0`, to have the operating system
assign a random port, which can be retrieved by using `server.address().port`
after the `'listening'` event has been emitted.

Backlog is the maximum length of the queue of pending connections.
The actual length will be determined by the OS through sysctl settings such as
`tcp_max_syn_backlog` and `somaxconn` on Linux. The default value of this
parameter is 511 (not 512).

This function is asynchronous.  When the server has been bound,
[`'listening'`][] event will be emitted.  The last parameter `callback`
will be added as a listener for the [`'listening'`][] event.

One issue some users run into is getting `EADDRINUSE` errors. This means that
another server is already running on the requested port. One way of handling this
would be to wait a second and then try again:

```js
server.on('error', (e) => {
  if (e.code == 'EADDRINUSE') {
    console.log('Address in use, retrying...');
    setTimeout(() => {
      server.close();
      server.listen(PORT, HOST);
    }, 1000);
  }
});
```

(Note: All sockets in Node.js are set `SO_REUSEADDR`.)

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

