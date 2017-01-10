<!-- YAML
added: v0.11.14
-->

* `options` {Object} - Required. Supports the following properties:
  * `port` {Number} - Required.
  * `address` {String} - Optional.
  * `exclusive` {Boolean} - Optional.
* `callback` {Function} - Optional.

For UDP sockets, causes the `dgram.Socket` to listen for datagram messages on a
named `port` and optional `address` that are passed as properties of an
`options` object passed as the first argument. If `port` is not specified, the
operating system will attempt to bind to a random port. If `address` is not
specified, the operating system will attempt to listen on all addresses.  Once
binding is complete, a `'listening'` event is emitted and the optional
`callback` function is called.

The `options` object may contain an additional `exclusive` property that is
use when using `dgram.Socket` objects with the [`cluster`] module. When
`exclusive` is set to `false` (the default), cluster workers will use the same
underlying socket handle allowing connection handling duties to be shared.
When `exclusive` is `true`, however, the handle is not shared and attempted
port sharing results in an error.

An example socket listening on an exclusive port is shown below.

```js
socket.bind({
  address: 'localhost',
  port: 8000,
  exclusive: true
});
```

