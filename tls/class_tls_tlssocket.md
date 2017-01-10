<!-- YAML
added: v0.11.4
-->

The `tls.TLSSocket` is a subclass of [`net.Socket`][] that performs transparent
encryption of written data and all required TLS negotiation.

Instances of `tls.TLSSocket` implement the duplex [Stream][] interface.

*Note*: Methods that return TLS connection metadata (e.g.
[`tls.TLSSocket.getPeerCertificate()`][] will only return data while the
connection is open.

