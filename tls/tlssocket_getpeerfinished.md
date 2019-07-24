<!-- YAML
added: v9.9.0
-->

* Returns: {Buffer|undefined} The latest `Finished` message that is expected
or has actually been received from the socket as part of a SSL/TLS handshake,
or `undefined` if there is no `Finished` message so far.

As the `Finished` messages are message digests of the complete handshake
(with a total of 192 bits for TLS 1.0 and more for SSL 3.0), they can
be used for external authentication procedures when the authentication
provided by SSL/TLS is not desired or is not enough.

Corresponds to the `SSL_get_peer_finished` routine in OpenSSL and may be used
to implement the `tls-unique` channel binding from [RFC 5929][].

