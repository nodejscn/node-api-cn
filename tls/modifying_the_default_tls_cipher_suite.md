
Node.js is built with a default suite of enabled and disabled TLS ciphers.
Currently, the default cipher suite is:

```txt
ECDHE-RSA-AES128-GCM-SHA256:
ECDHE-ECDSA-AES128-GCM-SHA256:
ECDHE-RSA-AES256-GCM-SHA384:
ECDHE-ECDSA-AES256-GCM-SHA384:
DHE-RSA-AES128-GCM-SHA256:
ECDHE-RSA-AES128-SHA256:
DHE-RSA-AES128-SHA256:
ECDHE-RSA-AES256-SHA384:
DHE-RSA-AES256-SHA384:
ECDHE-RSA-AES256-SHA256:
DHE-RSA-AES256-SHA256:
HIGH:
!aNULL:
!eNULL:
!EXPORT:
!DES:
!RC4:
!MD5:
!PSK:
!SRP:
!CAMELLIA
```

This default can be replaced entirely using the `--tls-cipher-list` command
line switch. For instance, the following makes
`ECDHE-RSA-AES128-GCM-SHA256:!RC4` the default TLS cipher suite:

```sh
node --tls-cipher-list="ECDHE-RSA-AES128-GCM-SHA256:!RC4"
```

The default can also be replaced on a per client or server basis using the
`ciphers` option from [`tls.createSecureContext()`][], which is also available
in [`tls.createServer()`], [`tls.connect()`], and when creating new
[`tls.TLSSocket`]s.

Consult [OpenSSL cipher list format documentation][] for details on the format.

*Note*: The default cipher suite included within Node.js has been carefully
selected to reflect current security best practices and risk mitigation.
Changing the default cipher suite can have a significant impact on the security
of an application. The `--tls-cipher-list` switch and `ciphers` option should by
used only if absolutely necessary.

The default cipher suite prefers GCM ciphers for [Chrome's 'modern
cryptography' setting] and also prefers ECDHE and DHE ciphers for Perfect
Forward Secrecy, while offering *some* backward compatibility.

128 bit AES is preferred over 192 and 256 bit AES in light of [specific
attacks affecting larger AES key sizes].

Old clients that rely on insecure and deprecated RC4 or DES-based ciphers
(like Internet Explorer 6) cannot complete the handshaking process with
the default configuration. If these clients _must_ be supported, the
[TLS recommendations] may offer a compatible cipher suite. For more details
on the format, see the [OpenSSL cipher list format documentation].

