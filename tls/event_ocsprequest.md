<!-- YAML
added: v0.11.13
-->

The `'OCSPRequest'` event is emitted when the client sends a certificate status
request. The listener callback is passed three arguments when called:

* `certificate` {Buffer} The server certificate
* `issuer` {Buffer} The issuer's certificate
* `callback` {Function} A callback function that must be invoked to provide
  the results of the OCSP request.

The server's current certificate can be parsed to obtain the OCSP URL
and certificate ID; after obtaining an OCSP response, `callback(null, resp)` is
then invoked, where `resp` is a `Buffer` instance containing the OCSP response.
Both `certificate` and `issuer` are `Buffer` DER-representations of the
primary and issuer's certificates. These can be used to obtain the OCSP
certificate ID and OCSP endpoint URL.

Alternatively, `callback(null, null)` may be called, indicating that there was
no OCSP response.

Calling `callback(err)` will result in a `socket.destroy(err)` call.

The typical flow of an OCSP Request is as follows:

1. Client connects to the server and sends an `'OCSPRequest'` (via the status
   info extension in ClientHello).
2. Server receives the request and emits the `'OCSPRequest'` event, calling the
   listener if registered.
3. Server extracts the OCSP URL from either the `certificate` or `issuer` and
   performs an [OCSP request] to the CA.
4. Server receives `OCSPResponse` from the CA and sends it back to the client
   via the `callback` argument
5. Client validates the response and either destroys the socket or performs a
   handshake.

*Note*: The `issuer` can be `null` if the certificate is either self-signed or
the issuer is not in the root certificates list. (An issuer may be provided
via the `ca` option when establishing the TLS connection.)

*Note*: Listening for this event will have an effect only on connections
established after the addition of the event listener.

*Note*: An npm module like [asn1.js] may be used to parse the certificates.

