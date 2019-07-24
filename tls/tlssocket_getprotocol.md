<!-- YAML
added: v5.7.0
-->

* Returns: {string|null}

Returns a string containing the negotiated SSL/TLS protocol version of the
current connection. The value `'unknown'` will be returned for connected
sockets that have not completed the handshaking process. The value `null` will
be returned for server sockets or disconnected client sockets.

Protocol versions are:

* `'TLSv1'`
* `'TLSv1.1'`
* `'TLSv1.2'`
* `'SSLv3'`

See <https://www.openssl.org/docs/man1.1.0/ssl/SSL_get_version.html> for more
information.

