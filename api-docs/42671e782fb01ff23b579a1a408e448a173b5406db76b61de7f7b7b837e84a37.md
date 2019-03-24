<!-- YAML
added: v6.0.0
-->

The `'tlsClientError'` event is emitted when an error occurs before a secure
connection is established. The listener callback is passed two arguments when
called:

* `exception` {Error} The `Error` object describing the error
* `tlsSocket` {tls.TLSSocket} The `tls.TLSSocket` instance from which the
  error originated.

