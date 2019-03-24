<!-- YAML
added: v0.11.4
changes:
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `socket` {net.Socket|stream.Duplex}
  On the server side, any `Duplex` stream. On the client side, any
  instance of [`net.Socket`][] (for generic `Duplex` stream support
  on the client side, [`tls.connect()`][] must be used).
* `options` {Object}
  * `isServer`: The SSL/TLS protocol is asymmetrical, TLSSockets must know if
    they are to behave as a server or a client. If `true` the TLS socket will be
    instantiated as a server. **Default:** `false`.
  * `server` {net.Server} A [`net.Server`][] instance.
  * `requestCert`: Whether to authenticate the remote peer by requesting a
     certificate. Clients always request a server certificate. Servers
     (`isServer` is true) may set `requestCert` to true to request a client
     certificate.
  * `rejectUnauthorized`: See [`tls.createServer()`][]
  * `ALPNProtocols`: See [`tls.createServer()`][]
  * `SNICallback`: See [`tls.createServer()`][]
  * `session` {Buffer} A `Buffer` instance containing a TLS session.
  * `requestOCSP` {boolean} If `true`, specifies that the OCSP status request
    extension will be added to the client hello and an `'OCSPResponse'` event
    will be emitted on the socket before establishing a secure communication
  * `secureContext`: TLS context object created with
    [`tls.createSecureContext()`][]. If a `secureContext` is _not_ provided, one
    will be created by passing the entire `options` object to
    `tls.createSecureContext()`.
  * ...: [`tls.createSecureContext()`][] options that are used if the
    `secureContext` option is missing. Otherwise, they are ignored.

Construct a new `tls.TLSSocket` object from an existing TCP socket.

