<!-- YAML
added: v0.3.4
-->

The HTTP Agent is used for pooling sockets used in HTTP client
requests.

The HTTP Agent also defaults client requests to using
`Connection: keep-alive`. If no pending HTTP requests are waiting on a
socket to become free the socket is closed. This means that Node.js's
pool has the benefit of keep-alive when under load but still does not
require developers to manually close the HTTP clients using
KeepAlive.

If you opt into using HTTP KeepAlive, you can create an Agent object
with that flag set to `true`.  (See the [constructor options][].)
Then, the Agent will keep unused sockets in a pool for later use.  They
will be explicitly marked so as to not keep the Node.js process running.
However, it is still a good idea to explicitly [`destroy()`][] KeepAlive
agents when they are no longer in use, so that the Sockets will be shut
down.

Sockets are removed from the agent's pool when the socket emits either
a `'close'` event or a special `'agentRemove'` event. This means that if
you intend to keep one HTTP request open for a long time and don't
want it to stay in the pool you can do something along the lines of:

```js
http.get(options, (res) => {
  // Do stuff
}).on('socket', (socket) => {
  socket.emit('agentRemove');
});
```

Alternatively, you could just opt out of pooling entirely using
`agent:false`:

```js
http.get({
  hostname: 'localhost',
  port: 80,
  path: '/',
  agent: false  // create a new agent just for this one request
}, (res) => {
  // Do stuff with response
});
```

