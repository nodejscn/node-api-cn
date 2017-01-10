
<!-- type=misc -->

The TLS protocol allows clients to renegotiate certain aspects of the TLS
session. Unfortunately, session renegotiation requires a disproportionate amount
of server-side resources, making it a potential vector for denial-of-service
attacks.

To mitigate the risk, renegotiation is limited to three times every ten minutes.
An `'error'` event is emitted on the [`tls.TLSSocket`][] instance when this
threshold is exceeded. The limits are configurable:

* `tls.CLIENT_RENEG_LIMIT` {number} Specifies the number of renegotiation
  requests. Defaults to `3`.
* `tls.CLIENT_RENEG_WINDOW` {number} Specifies the time renegotiation window
  in seconds. Defaults to `600` (10 minutes).

*Note*: The default renegotiation limits should not be modified without a full
understanding of the implications and risks.

To test the renegotiation limits on a server, connect to it using the OpenSSL
command-line client (`openssl s_client -connect address:port`) then input
`R<CR>` (i.e., the letter `R` followed by a carriage return) multiple times.

