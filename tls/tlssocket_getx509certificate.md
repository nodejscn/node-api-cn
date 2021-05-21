<!-- YAML
added: v15.9.0
-->

* Returns: {X509Certificate}

Returns the local certificate as an {X509Certificate} object.

If there is no local certificate, or the socket has been destroyed,
`undefined` will be returned.

