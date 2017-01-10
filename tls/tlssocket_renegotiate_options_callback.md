<!-- YAML
added: v0.11.8
-->

* `options` {Object}
  * `rejectUnauthorized` {boolean}
  * `requestCert`
* `callback` {Function} A function that will be called when the renegotiation
  request has been completed.

The `tlsSocket.renegotiate()` method initiates a TLS renegotiation process.
Upon completion, the `callback` function will be passed a single argument
that is either an `Error` (if the request failed) or `null`.

*Note*: This method can be used to request a peer's certificate after the
secure connection has been established.

*Note*: When running as the server, the socket will be destroyed with an error
after `handshakeTimeout` timeout.

