<!-- YAML
added: v0.1.99
-->

* `port` {Number} - Integer, Optional
* `address` {String}, Optional
* `callback` {Function} with no parameters, Optional. Called when
  binding is complete.

For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a
named `port` and optional `address`. If `port` is not specified, the operating
system will attempt to bind to a random port. If `address` is not specified,
the operating system will attempt to listen on all addresses.  Once binding is
complete, a `'listening'` event is emitted and the optional `callback` function
is called.

Note that specifying both a `'listening'` event listener and passing a
`callback` to the `socket.bind()` method is not harmful but not very
useful.

A bound datagram socket keeps the Node.js process running to receive
datagram messages.

If binding fails, an `'error'` event is generated. In rare case (e.g.
attempting to bind with a closed socket), an [`Error`][] may be thrown.

Example of a UDP server listening on port 41234:

```js
const dgram = require('dgram');
const server = dgram.createSocket('udp4');

server.on('error', (err) => {
  console.log(`server error:\n${err.stack}`);
  server.close();
});

server.on('message', (msg, rinfo) => {
  console.log(`server got: ${msg} from ${rinfo.address}:${rinfo.port}`);
});

server.on('listening', () => {
  var address = server.address();
  console.log(`server listening ${address.address}:${address.port}`);
});

server.bind(41234);
// server listening 0.0.0.0:41234
```

