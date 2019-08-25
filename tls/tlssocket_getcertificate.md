<!-- YAML
added: v11.2.0
-->

* Returns: {Object}

Returns an object representing the local certificate. The returned object has
some properties corresponding to the fields of the certificate.

See [`tls.TLSSocket.getPeerCertificate()`][] for an example of the certificate
structure.

If there is no local certificate, an empty object will be returned. If the
socket has been destroyed, `null` will be returned.

