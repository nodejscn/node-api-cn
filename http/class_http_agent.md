<!-- YAML
added: v0.3.4
-->

An `Agent` is responsible for managing connection persistence
and reuse for HTTP clients. It maintains a queue of pending requests
for a given host and port, reusing a single socket connection for each
until the queue is empty, at which time the socket is either destroyed
or put into a pool where it is kept to be used again for requests to the
same host and port. Whether it is destroyed or pooled depends on the
`keepAlive` [option](#http_new_agent_options).

Pooled connections have TCP Keep-Alive enabled for them, but servers may
still close idle connections, in which case they will be removed from the
pool and a new connection will be made when a new HTTP request is made for
that host and port. Servers may also refuse to allow multiple requests
over the same connection, in which case the connection will have to be
remade for every request and cannot be pooled. The `Agent` will still make
the requests to that server, but each one will occur over a new connection.

When a connection is closed by the client or the server, it is removed
from the pool. Any unused sockets in the pool will be unrefed so as not
to keep the Node.js process running when there are no outstanding requests.
(see [socket.unref()]).

It is good practice, to [`destroy()`][] an `Agent` instance when it is no
longer in use, because unused sockets consume OS resources.

Sockets are removed from an agent's pool when the socket emits either
a `'close'` event or an `'agentRemove'` event. This means that if
you intend to keep one HTTP request open for a long time and don't
want it to stay in the pool you can do something along the lines of:

```js
http.get(options, (res) => {
  // 处理事情
}).on('socket', (socket) => {
  socket.emit('agentRemove');
});
```

You may also use an agent for an individual request. By providing
`{agent: false}` as an option to the `http.get()` or `http.request()`
functions, a one-time use `Agent` with default options will be used
for the client connection.

`agent:false`:

```js
http.get({
  hostname: 'localhost',
  port: 80,
  path: '/',
  agent: false  // 创建一个新的代理，只用于本次请求
}, (res) => {
  // 对响应进行处理
});
```

