
Similarly, the `sendHandler` argument can be used to pass the handle of a
socket to the child process. The example below spawns two children that each
handle connections with "normal" or "special" priority:

```js
const normal = require('child_process').fork('child.js', ['normal']);
const special = require('child_process').fork('child.js', ['special']);

// Open up the server and send sockets to child
const server = require('net').createServer();
server.on('connection', (socket) => {

  // If this is special priority
  if (socket.remoteAddress === '74.125.127.100') {
    special.send('socket', socket);
    return;
  }
  // This is normal priority
  normal.send('socket', socket);
});
server.listen(1337);
```

The `child.js` would receive the socket handle as the second argument passed
to the event callback function:

```js
process.on('message', (m, socket) => {
  if (m === 'socket') {
    socket.end(`Request handled with ${process.argv[2]} priority`);
  }
});
```

Once a socket has been passed to a child, the parent is no longer capable of
tracking when the socket is destroyed. To indicate this, the `.connections`
property becomes `null`. It is recommended not to use `.maxConnections` when
this occurs.

*Note: this function uses [`JSON.stringify()`][] internally to serialize the
`message`.*

