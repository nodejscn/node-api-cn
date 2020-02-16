
<!-- type=misc -->

TLS-PSK support is available as an alternative to normal certificate-based
authentication. It uses a pre-shared key instead of certificates to
authenticate a TLS connection, providing mutual authentication.
TLS-PSK and public key infrastructure are not mutually exclusive. Clients and
servers can accommodate both, choosing either of them during the normal cipher
negotiation step.

TLS-PSK is only a good choice where means exist to securely share a
key with every connecting machine, so it does not replace PKI
(Public Key Infrastructure) for the majority of TLS uses.
The TLS-PSK implementation in OpenSSL has seen many security flaws in
recent years, mostly because it is used only by a minority of applications.
Please consider all alternative solutions before switching to PSK ciphers.
Upon generating PSK it is of critical importance to use sufficient entropy as
discussed in [RFC 4086][]. Deriving a shared secret from a password or other
low-entropy sources is not secure.

PSK ciphers are disabled by default, and using TLS-PSK thus requires explicitly
specifying a cipher suite with the `ciphers` option. The list of available
ciphers can be retrieved via `openssl ciphers -v 'PSK'`. All TLS 1.3
ciphers are eligible for PSK but currently only those that use SHA256 digest are
supported they can be retrieved via `openssl ciphers -v -s -tls1_3 -psk`.

According to the [RFC 4279][], PSK identities up to 128 bytes in length and
PSKs up to 64 bytes in length must be supported. As of OpenSSL 1.1.0
maximum identity size is 128 bytes, and maximum PSK length is 256 bytes.

The current implementation doesn't support asynchronous PSK callbacks due to the
limitations of the underlying OpenSSL API.

