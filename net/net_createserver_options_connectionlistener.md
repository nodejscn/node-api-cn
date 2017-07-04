<!-- YAML
added: v0.5.0
-->

Creates a new TCP or [IPC][] server.

* `options` {Object}
  * `allowHalfOpen` {boolean} Default to `false`. Indicates whether half-opened
    TCP connections are allowed.
  * `pauseOnConnect` {boolean} Default to `false`. Indicates whether the socket
    should be paused on incoming connections.
* `connectionListener` {Function} Automatically set as a listener for the
  [`'connection'`][] event
* Returns: {net.Server}

If `allowHalfOpen` is set to `true`, when the other end of the socket
sends a FIN packet, the server will only send a FIN packet back when
[`socket.end()`][] is explicitly called, until then the connection is
half-closed (non-readable but still writable). See [`'end'`][] event
and [RFC 1122][half-closed] for more information.

If `pauseOnConnect` is set to `true`, then the socket associated with each
incoming connection will be paused, and no data will be read from its handle.
This allows connections to be passed between processes without any data being
read by the original process. To begin reading data from a paused socket, call
[`socket.resume()`][].

The server can be a TCP server or a [IPC][] server, depending on what it
[`listen()`][`server.listen()`] to.

Here is an example of an TCP echo server which listens for connections
on port 8124:

```js
const net = require('net');
const server = net.createServer((c) => {
  // 'connection' listener
  console.log('client connected');
  c.on('end', () => {
    console.log('client disconnected');
  });
  c.write('hello\r\n');
  c.pipe(c);
});
server.on('error', (err) => {
  throw err;
});
server.listen(8124, () => {
  console.log('server bound');
});
```

Test this by using `telnet`:

```console
$ telnet localhost 8124
```

To listen on the socket `/tmp/echo.sock` the third line from the last would
just be changed to

```js
server.listen('/tmp/echo.sock', () => {
  console.log('server bound');
});
```

Use `nc` to connect to a UNIX domain socket server:

```console
$ nc -U /tmp/echo.sock
```

