
The `sendHandle` argument can be used, for instance, to pass the handle of
a TCP server object to the child process as illustrated in the example below:

```js
const child = require('child_process').fork('child.js');

// Open up the server object and send the handle.
const server = require('net').createServer();
server.on('connection', (socket) => {
  socket.end('handled by parent');
});
server.listen(1337, () => {
  child.send('server', server);
});
```

The child would then receive the server object as:

```js
process.on('message', (m, server) => {
  if (m === 'server') {
    server.on('connection', (socket) => {
      socket.end('handled by child');
    });
  }
});
```

Once the server is now shared between the parent and child, some connections
can be handled by the parent and some by the child.

While the example above uses a server created using the `net` module, `dgram`
module servers use exactly the same workflow with the exceptions of listening on
a `'message'` event instead of `'connection'` and using `server.bind()` instead of
`server.listen()`. This is, however, currently only supported on UNIX platforms.

