<!-- YAML
added: v0.3.2
deprecated: v0.11.3
-->

> Stability: 0 - Deprecated: Use [`tls.TLSSocket`][] instead.

* `context` {Object} A secure context object as returned by
  `tls.createSecureContext()`
* `isServer` {boolean} `true` to specify that this TLS connection should be
  opened as a server.
* `requestCert` {boolean} `true` to specify whether a server should request a
  certificate from a connecting client. Only applies when `isServer` is `true`.
* `rejectUnauthorized` {boolean} `true` to specify whether a server should
  automatically reject clients with invalid certificates. Only applies when
  `isServer` is `true`.
* `options`
  * `secureContext`: An optional TLS context object from
     [`tls.createSecureContext()`][]
  * `isServer`: If `true` the TLS socket will be instantiated in server-mode.
    Defaults to `false`.
  * `server` {net.Server} An optional [`net.Server`][] instance
  * `requestCert`: Optional, see [`tls.createServer()`][]
  * `rejectUnauthorized`: Optional, see [`tls.createServer()`][]
  * `NPNProtocols`: Optional, see [`tls.createServer()`][]
  * `ALPNProtocols`: Optional, see [`tls.createServer()`][]
  * `SNICallback`: Optional, see [`tls.createServer()`][]
  * `session` {Buffer} An optional `Buffer` instance containing a TLS session.
  * `requestOCSP` {boolean} If `true`, specifies that the OCSP status request
    extension will be added to the client hello and an `'OCSPResponse'` event
    will be emitted on the socket before establishing a secure communication

Creates a new secure pair object with two streams, one of which reads and writes
the encrypted data and the other of which reads and writes the cleartext data.
Generally, the encrypted stream is piped to/from an incoming encrypted data
stream and the cleartext one is used as a replacement for the initial encrypted
stream.

`tls.createSecurePair()` returns a `tls.SecurePair` object with `cleartext` and
`encrypted` stream properties.

*Note*: `cleartext` has the same API as [`tls.TLSSocket`][].

*Note*: The `tls.createSecurePair()` method is now deprecated in favor of
`tls.TLSSocket()`. For example, the code:

```js
pair = tls.createSecurePair( ... );
pair.encrypted.pipe(socket);
socket.pipe(pair.encrypted);
```

can be replaced by:

```js
secure_socket = tls.TLSSocket(socket, options);
```

where `secure_socket` has the same API as `pair.cleartext`.

[OpenSSL cipher list format documentation]: https://www.openssl.org/docs/man1.0.2/apps/ciphers.html#CIPHER-LIST-FORMAT
[Chrome's 'modern cryptography' setting]: https://www.chromium.org/Home/chromium-security/education/tls#TOC-Cipher-Suites
[OpenSSL Options]: crypto.html#crypto_openssl_options
[modifying the default cipher suite]: #tls_modifying_the_default_tls_cipher_suite
[specific attacks affecting larger AES key sizes]: https://www.schneier.com/blog/archives/2009/07/another_new_aes.html
[`crypto.getCurves()`]: crypto.html#crypto_crypto_getcurves
[`tls.createServer()`]: #tls_tls_createserver_options_secureconnectionlistener
[`tls.createSecurePair()`]: #tls_tls_createsecurepair_context_isserver_requestcert_rejectunauthorized_options
[`tls.TLSSocket`]: #tls_class_tls_tlssocket
[`net.Server`]: net.html#net_class_net_server
[`net.Socket`]: net.html#net_class_net_socket
[`net.Server.address()`]: net.html#net_server_address
[`'secureConnect'`]: #tls_event_secureconnect
[`'secureConnection'`]: #tls_event_secureconnection
[Perfect Forward Secrecy]: #tls_perfect_forward_secrecy
[Stream]: stream.html#stream_stream
[SSL_METHODS]: https://www.openssl.org/docs/man1.0.2/ssl/ssl.html#DEALING-WITH-PROTOCOL-METHODS
[tls.Server]: #tls_class_tls_server
[SSL_CTX_set_timeout]: https://www.openssl.org/docs/man1.0.2/ssl/SSL_CTX_set_timeout.html
[Forward secrecy]: https://en.wikipedia.org/wiki/Perfect_forward_secrecy
[DHE]: https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange
[ECDHE]: https://en.wikipedia.org/wiki/Elliptic_curve_Diffie%E2%80%93Hellman
[asn1.js]: https://npmjs.org/package/asn1.js
[OCSP request]: https://en.wikipedia.org/wiki/OCSP_stapling
[TLS recommendations]: https://wiki.mozilla.org/Security/Server_Side_TLS
[TLS Session Tickets]: https://www.ietf.org/rfc/rfc5077.txt
[`tls.TLSSocket.getPeerCertificate()`]: #tls_tlssocket_getpeercertificate_detailed
[`tls.createSecureContext()`]: #tls_tls_createsecurecontext_options
[`tls.connect()`]: #tls_tls_connect_options_callback
