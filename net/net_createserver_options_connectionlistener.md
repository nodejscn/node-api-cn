<!-- YAML
added: v0.5.0
-->

Creates a new server. The `connectionListener` argument is
automatically set as a listener for the [`'connection'`][] event.

`options` is an object with the following defaults:

```js
{
  allowHalfOpen: false,
  pauseOnConnect: false
}
```

If `allowHalfOpen` is `true`, then the socket won't automatically send a FIN
packet when the other end of the socket sends a FIN packet. The socket becomes
non-readable, but still writable. You should call the [`end()`][] method explicitly.
See [`'end'`][] event for more information.

If `pauseOnConnect` is `true`, then the socket associated with each incoming
connection will be paused, and no data will be read from its handle. This allows
connections to be passed between processes without any data being read by the
original process. To begin reading data from a paused socket, call [`resume()`][].

Here is an example of an echo server which listens for connections
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

```sh
telnet localhost 8124
```

To listen on the socket `/tmp/echo.sock` the third line from the last would
just be changed to

```js
server.listen('/tmp/echo.sock', () => {
  console.log('server bound');
});
```

Use `nc` to connect to a UNIX domain socket server:

```js
nc -U /tmp/echo.sock
```

