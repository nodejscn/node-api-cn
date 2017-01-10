<!-- YAML
added: v0.11.14
-->

* `options` {Object} - Required. Supports the following properties:
  * `port` {Number} - Optional.
  * `host` {String} - Optional.
  * `backlog` {Number} - Optional.
  * `path` {String} - Optional.
  * `exclusive` {Boolean} - Optional.
* `callback` {Function} - Optional.

The `port`, `host`, and `backlog` properties of `options`, as well as the
optional callback function, behave as they do on a call to
[`server.listen([port][, hostname][, backlog][, callback])`][`server.listen(port, host, backlog, callback)`].
Alternatively, the `path` option can be used to specify a UNIX socket.

If `exclusive` is `false` (default), then cluster workers will use the same
underlying handle, allowing connection handling duties to be shared. When
`exclusive` is `true`, the handle is not shared, and attempted port sharing
results in an error. An example which listens on an exclusive port is
shown below.

```js
server.listen({
  host: 'localhost',
  port: 80,
  exclusive: true
});
```

*Note*: The `server.listen()` method may be called multiple times. Each
subsequent call will *re-open* the server using the provided options.

