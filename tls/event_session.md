<!-- YAML
added: v11.10.0
-->

* `session` {Buffer}

The `'session'` event is emitted on a client `tls.TLSSocket` when a new session
or TLS ticket is available. This may or may not be before the handshake is
complete, depending on the TLS protocol version that was negotiated. The event
is not emitted on the server, or if a new session was not created, for example,
when the connection was resumed. For some TLS protocol versions the event may be
emitted multiple times, in which case all the sessions can be used for
resumption.

On the client, the `session` can be provided to the `session` option of
[`tls.connect()`][] to resume the connection.

See [Session Resumption][] for more information.

For TLSv1.2 and below, [`tls.TLSSocket.getSession()`][] can be called once
the handshake is complete. For TLSv1.3, only ticket-based resumption is allowed
by the protocol, multiple tickets are sent, and the tickets aren't sent until
after the handshake completes. So it is necessary to wait for the
`'session'` event to get a resumable session. Applications
should use the `'session'` event instead of `getSession()` to ensure
they will work for all TLS versions. Applications that only expect to
get or use one session should listen for this event only once:

```js
tlsSocket.once('session', (session) => {
  // The session can be used immediately or later.
  tls.connect({
    session: session,
    // Other connect options...
  });
});
```

