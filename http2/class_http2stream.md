<!-- YAML
added: v8.4.0
-->

* 继承自: {stream.Duplex}

Each instance of the `Http2Stream` class represents a bidirectional HTTP/2
communications stream over an `Http2Session` instance. Any single `Http2Session`
may have up to 2<sup>31</sup>-1 `Http2Stream` instances over its lifetime.

User code will not construct `Http2Stream` instances directly. Rather, these
are created, managed, and provided to user code through the `Http2Session`
instance. On the server, `Http2Stream` instances are created either in response
to an incoming HTTP request (and handed off to user code via the `'stream'`
event), or in response to a call to the `http2stream.pushStream()` method.
On the client, `Http2Stream` instances are created and returned when either the
`http2session.request()` method is called, or in response to an incoming
`'push'` event.

The `Http2Stream` class is a base for the [`ServerHttp2Stream`][] and
[`ClientHttp2Stream`][] classes, each of which is used specifically by either
the Server or Client side, respectively.

All `Http2Stream` instances are [`Duplex`][] streams. The `Writable` side of the
`Duplex` is used to send data to the connected peer, while the `Readable` side
is used to receive data sent by the connected peer.

The default text character encoding for all `Http2Stream`s is UTF-8. As a best
practice, it is recommended that when using an `Http2Stream` to send text,
the `'content-type'` header should be set and should identify the character
encoding used.

```js
stream.respond({
  'content-type': 'text/html; charset=utf-8',
  ':status': 200
});
```

