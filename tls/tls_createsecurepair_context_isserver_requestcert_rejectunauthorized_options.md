<!-- YAML
added: v0.3.2
deprecated: v0.11.3
changes:
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

> Stability: 0 - Deprecated: Use [`tls.TLSSocket`][] instead.

* `context` {Object} A secure context object as returned by
  `tls.createSecureContext()`
* `isServer` {boolean} `true` to specify that this TLS connection should be
  opened as a server.
* `requestCert` {boolean} `true` to specify whether a server should request a
  certificate from a connecting client. Only applies when `isServer` is `true`.
* `rejectUnauthorized` {boolean} If not `false` a server automatically reject clients
   with invalid certificates. Only applies when `isServer` is `true`.
* `options`
  * `secureContext`: An optional TLS context object from
     [`tls.createSecureContext()`][]
  * `isServer`: If `true` the TLS socket will be instantiated in server-mode.
    Defaults to `false`.
  * `server` {net.Server} An optional [`net.Server`][] instance
  * `requestCert`: Optional, see [`tls.createServer()`][]
  * `rejectUnauthorized`: Optional, see [`tls.createServer()`][]
  * `NPNProtocols`: Optional, see [`tls.createServer()`][]
  * `ALPNProtocols`: Optional, see [`tls.createServer()`][]
  * `SNICallback`: Optional, see [`tls.createServer()`][]
  * `session` {Buffer} An optional `Buffer` instance containing a TLS session.
  * `requestOCSP` {boolean} If `true`, specifies that the OCSP status request
    extension will be added to the client hello and an `'OCSPResponse'` event
    will be emitted on the socket before establishing a secure communication

Creates a new secure pair object with two streams, one of which reads and writes
the encrypted data and the other of which reads and writes the cleartext data.
Generally, the encrypted stream is piped to/from an incoming encrypted data
stream and the cleartext one is used as a replacement for the initial encrypted
stream.

`tls.createSecurePair()` returns a `tls.SecurePair` object with `cleartext` and
`encrypted` stream properties.

*Note*: `cleartext` has the same API as [`tls.TLSSocket`][].

*Note*: The `tls.createSecurePair()` method is now deprecated in favor of
`tls.TLSSocket()`. For example, the code:

```js
pair = tls.createSecurePair(/* ... */);
pair.encrypted.pipe(socket);
socket.pipe(pair.encrypted);
```

can be replaced by:

```js
secure_socket = tls.TLSSocket(socket, options);
```

where `secure_socket` has the same API as `pair.cleartext`.
