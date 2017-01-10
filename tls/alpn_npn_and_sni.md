
<!-- type=misc -->

ALPN (Application-Layer Protocol Negotiation Extension), NPN (Next
Protocol Negotiation) and, SNI (Server Name Indication) are TLS
handshake extensions:

* ALPN/NPN - Allows the use of one TLS server for multiple protocols (HTTP,
  SPDY, HTTP/2)
* SNI - Allows the use of one TLS server for multiple hostnames with different
  SSL certificates.

*Note*: Use of ALPN is recommended over NPN. The NPN extension has never been
formally defined or documented and generally not recommended for use.

