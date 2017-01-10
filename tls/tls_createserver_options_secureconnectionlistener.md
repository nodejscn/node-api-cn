<!-- YAML
added: v0.3.2
-->

* `options` {Object}
  * `pfx` {string|Buffer} A string or `Buffer` containing the private key,
    certificate and CA certs of the server in PFX or PKCS12 format. (Mutually
    exclusive with the `key`, `cert`, and `ca` options.)
  * `key` {string|string[]|Buffer|Object[]} The private key of the server in
    PEM format. To support multiple keys using different algorithms an array can
    be provided either as a plain array of key strings or an array of objects
    in the format `{pem: key, passphrase: passphrase}`. This option is
    *required* for ciphers that make use of private keys.
  * `passphrase` {string} A string containing the passphrase for the private
    key or pfx.
  * `cert` {string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of
    strings, or array of `Buffer`s containing the certificate key of the server
    in PEM format. (Required)
  * `ca` {string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of strings,
    or array of `Buffer`s of trusted certificates in PEM format. If this is
    omitted several well known "root" CAs (like VeriSign) will be used. These
    are used to authorize connections.
  * `crl` {string|string[]} Either a string or array of strings of PEM encoded
    CRLs (Certificate Revocation List).
  * `ciphers` {string} A string describing the ciphers to use or exclude,
    separated by `:`.
  * `ecdhCurve` {string} A string describing a named curve to use for ECDH key
    agreement or `false` to disable ECDH. Defaults to `prime256v1` (NIST P-256).
    Use [`crypto.getCurves()`][] to obtain a list of available curve names. On
    recent releases, `openssl ecparam -list_curves` will also display the name
    and description of each available elliptic curve.
  * `dhparam` {string|Buffer} A string or `Buffer` containing Diffie Hellman
    parameters, required for [Perfect Forward Secrecy][]. Use
    `openssl dhparam` to create the parameters. The key length must be greater
    than or equal to 1024 bits, otherwise an error will be thrown. It is
    strongly recommended to use 2048 bits or larger for stronger security. If
    omitted or invalid, the parameters are silently discarded and DHE ciphers
    will not be available.
  * `handshakeTimeout` {number} Abort the connection if the SSL/TLS handshake
    does not finish in the specified number of milliseconds. Defaults to `120`
    seconds. A `'clientError'` is emitted on the `tls.Server` object whenever a
    handshake times out.
  * `honorCipherOrder` {boolean} When choosing a cipher, use the server's
    preferences instead of the client preferences. Defaults to `true`.
  * `requestCert` {boolean} If `true` the server will request a certificate from
    clients that connect and attempt to verify that certificate. Defaults to
    `false`.
  * `rejectUnauthorized` {boolean} If `true` the server will reject any
    connection which is not authorized with the list of supplied CAs. This
    option only has an effect if `requestCert` is `true`. Defaults to `false`.
  * `NPNProtocols` {string[]|Buffer} An array of strings or a `Buffer` naming
    possible NPN protocols. (Protocols should be ordered by their priority.)
  * `ALPNProtocols` {string[]|Buffer} An array of strings or a `Buffer` naming
    possible ALPN protocols. (Protocols should be ordered by their priority.)
    When the server receives both NPN and ALPN extensions from the client,
    ALPN takes precedence over NPN and the server does not send an NPN
    extension to the client.
  * `SNICallback(servername, cb)` {Function} A function that will be called if
    the client supports SNI TLS extension. Two arguments will be passed when
    called: `servername` and `cb`. `SNICallback` should invoke `cb(null, ctx)`,
    where `ctx` is a SecureContext instance. (`tls.createSecureContext(...)` can
    be used to get a proper SecureContext.) If `SNICallback` wasn't provided the
    default callback with high-level API will be used (see below).
  * `sessionTimeout` {number} An integer specifying the number of seconds after
    which the TLS session identifiers and TLS session tickets created by the
    server will time out. See [SSL_CTX_set_timeout] for more details.
  * `ticketKeys`: A 48-byte `Buffer` instance consisting of a 16-byte prefix,
    a 16-byte HMAC key, and a 16-byte AES key. This can be used to accept TLS
    session tickets on multiple instances of the TLS server. *Note* that this is
    automatically shared between `cluster` module workers.
  * `sessionIdContext` {string} A string containing an opaque identifier for
    session resumption. If `requestCert` is `true`, the default is a 128 bit
    truncated SHA1 hash value generated from the command-line. Otherwise, a
    default is not provided.
  * `secureProtocol` {string} The SSL method to use, e.g. `SSLv3_method` to
    force SSL version 3. The possible values depend on the version of OpenSSL
    installed in the environment and are defined in the constant
    [SSL_METHODS][].
* `secureConnectionListener` {Function}

Creates a new [tls.Server][].  The `secureConnectionListener`, if provided, is
automatically set as a listener for the [`'secureConnection'`][] event.

For the `ciphers` option, the default cipher suite is:

```text
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

The following illustrates a simple echo server:

```js
const tls = require('tls');
const fs = require('fs');

const options = {
  key: fs.readFileSync('server-key.pem'),
  cert: fs.readFileSync('server-cert.pem'),

  // This is necessary only if using the client certificate authentication.
  requestCert: true,

  // This is necessary only if the client uses the self-signed certificate.
  ca: [ fs.readFileSync('client-cert.pem') ]
};

const server = tls.createServer(options, (socket) => {
  console.log('server connected',
              socket.authorized ? 'authorized' : 'unauthorized');
  socket.write('welcome!\n');
  socket.setEncoding('utf8');
  socket.pipe(socket);
});
server.listen(8000, () => {
  console.log('server bound');
});
```

Or

```js
const tls = require('tls');
const fs = require('fs');

const options = {
  pfx: fs.readFileSync('server.pfx'),

  // This is necessary only if using the client certificate authentication.
  requestCert: true,

};

const server = tls.createServer(options, (socket) => {
  console.log('server connected',
              socket.authorized ? 'authorized' : 'unauthorized');
  socket.write('welcome!\n');
  socket.setEncoding('utf8');
  socket.pipe(socket);
});
server.listen(8000, () => {
  console.log('server bound');
});
```

This server can be tested by connecting to it using `openssl s_client`:

```sh
openssl s_client -connect 127.0.0.1:8000
```

