<!-- YAML
added: v8.4.0
-->

* {net.Socket}

The [`net.Socket`][] object associated with the connection.

With TLS support, use [`request.socket.getPeerCertificate()`][] to obtain the
client's authentication details.

*Note*: do not use this socket object to send or receive any data. All
data transfers are managed by HTTP/2 and data might be lost.

