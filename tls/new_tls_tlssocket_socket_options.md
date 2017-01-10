<!-- YAML
added: v0.11.4
-->

* `socket` {net.Socket} An instance of [`net.Socket`][]
* `options` {Object}
  * `secureContext`: An optional TLS context object from
     [`tls.createSecureContext()`][]
  * `isServer`: If `true` the TLS socket will be instantiated in server-mode.
    Defaults to `false`.
  * `server` {net.Server} An optional [`net.Server`][] instance.
  * `requestCert`: Optional, see [`tls.createServer()`][]
  * `rejectUnauthorized`: Optional, see [`tls.createServer()`][]
  * `NPNProtocols`: Optional, see [`tls.createServer()`][]
  * `ALPNProtocols`: Optional, see [`tls.createServer()`][]
  * `SNICallback`: Optional, see [`tls.createServer()`][]
  * `session` {Buffer} An optional `Buffer` instance containing a TLS session.
  * `requestOCSP` {boolean} If `true`, specifies that the OCSP status request
    extension will be added to the client hello and an `'OCSPResponse'` event
    will be emitted on the socket before establishing a secure communication

Construct a new `tls.TLSSocket` object from an existing TCP socket.

