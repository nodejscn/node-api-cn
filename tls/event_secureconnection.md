<!-- YAML
added: v0.3.2
-->

The `'secureConnection'` event is emitted after the handshaking process for a
new connection has successfully completed. The listener callback is passed a
single argument when called:

* `tlsSocket` {tls.TLSSocket} The established TLS socket.

The `tlsSocket.authorized` property is a `boolean` indicating whether the
client has been verified by one of the supplied Certificate Authorities for the
server. If `tlsSocket.authorized` is `false`, then `socket.authorizationError`
is set to describe how authorization failed. Note that depending on the settings
of the TLS server, unauthorized connections may still be accepted.

The `tlsSocket.npnProtocol` and `tlsSocket.alpnProtocol` properties are strings
that contain the selected NPN and ALPN protocols, respectively. When both NPN
and ALPN extensions are received, ALPN takes precedence over NPN and the next
protocol is selected by ALPN.

When ALPN has no selected protocol, `tlsSocket.alpnProtocol` returns `false`.

The `tlsSocket.servername` property is a string containing the server name
requested via SNI.

