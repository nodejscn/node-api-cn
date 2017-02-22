
<!-- type=misc -->

The term "[Forward Secrecy]" or "Perfect Forward Secrecy" describes a feature of
key-agreement (i.e., key-exchange) methods. That is, the server and client keys
are used to negotiate new temporary keys that are used specifically and only for
the current communication session. Practically, this means that even if the
server's private key is compromised, communication can only be decrypted by
eavesdroppers if the attacker manages to obtain the key-pair specifically
generated for the session.

Perfect Forward Secrecy is achieved by randomly generating a key pair for
key-agreement on every TLS/SSL handshake (in contrast to using the same key for
all sessions). Methods implementing this technique are called "ephemeral".

Currently two methods are commonly used to achieve Perfect Forward Secrecy (note
the character "E" appended to the traditional abbreviations):

* [DHE] - An ephemeral version of the Diffie Hellman key-agreement protocol.
* [ECDHE] - An ephemeral version of the Elliptic Curve Diffie Hellman
  key-agreement protocol.

Ephemeral methods may have some performance drawbacks, because key generation
is expensive.

To use Perfect Forward Secrecy using `DHE` with the `tls` module, it is required
to generate Diffie-Hellman parameters and specify them with the `dhparam`
option to [`tls.createSecureContext()`][]. The following illustrates the use of
the OpenSSL command-line interface to generate such parameters:

```sh
openssl dhparam -outform PEM -out dhparam.pem 2048
```

If using Perfect Forward Secrecy using `ECDHE`, Diffie-Hellman parameters are
not required and a default ECDHE curve will be used. The `ecdhCurve` property
can be used when creating a TLS Server to specify the name of an alternative
curve to use, see [`tls.createServer()`] for more info.

