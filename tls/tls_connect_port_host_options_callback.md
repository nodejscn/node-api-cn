<!-- YAML
added: v0.11.3
-->

* `port` {number}
* `host` {string}
* `options` {Object}
  * `host` {string} Host the client should connect to.
  * `port` {number} Port the client should connect to.
  * `socket` {net.Socket} Establish secure connection on a given socket rather
    than creating a new socket. If this option is specified, `host` and `port`
    are ignored.
  * `path` {string} Creates unix socket connection to path. If this option is
    specified, `host` and `port` are ignored.
  * `pfx` {string|Buffer} A string or `Buffer` containing the private key,
    certificate, and CA certs of the client in PFX or PKCS12 format.
  * `key` {string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of
    strings, or array of `Buffer`s containing the private key of the client in
    PEM format.
  * `passphrase` {string} A string containing the passphrase for the private key
    or pfx.
  * `cert` {string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of
    strings, or array of `Buffer`s containing the certificate key of the client
    in PEM format.
  * `ca` {string|string[]|Buffer|Buffer[]} A string, `Buffer`, array of strings,
    or array of `Buffer`s of trusted certificates in PEM format. If this is
    omitted several well known "root" CAs (like VeriSign) will be used. These
    are used to authorize connections.
  * `ciphers` {string} A string describing the ciphers to use or exclude,
    separated by `:`. Uses the same default cipher suite as
    [`tls.createServer()`][].
  * `rejectUnauthorized` {boolean} If `true`, the server certificate is verified
    against the list of supplied CAs. An `'error'` event is emitted if
    verification fails; `err.code` contains the OpenSSL error code. Defaults to
    `true`.
  * `NPNProtocols` {string[]|Buffer[]} An array of strings or `Buffer`s
    containing supported NPN protocols. `Buffer`s should have the format
    `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the first
    byte is the length of the next protocol name. Passing an array is usually
    much simpler, e.g. `['hello', 'world']`.
  * `ALPNProtocols`: {string[]|Buffer[]} An array of strings or `Buffer`s
    containing the supported ALPN protocols. `Buffer`s should have the format
    `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the first byte
    is the length of the next protocol name. Passing an array is usually much
    simpler: `['hello', 'world']`.)
  * `servername`: {string} Server name for the SNI (Server Name Indication) TLS
    extension.
  * `checkServerIdentity(servername, cert)` {Function} A callback function
    to be used when checking the server's hostname against the certificate.
    This should throw an error if verification fails. The method should return
    `undefined` if the `servername` and `cert` are verified.
  * `secureProtocol` {string} The SSL method to use, e.g. `SSLv3_method` to
    force SSL version 3. The possible values depend on the version of OpenSSL
    installed in the environment and are defined in the constant
    [SSL_METHODS][].
  * `secureContext` {object} An optional TLS context object as returned by from
    `tls.createSecureContext( ... )`. It can be used for caching client
    certificates, keys, and CA certificates.
  * `session` {Buffer} A `Buffer` instance, containing TLS session.
  * `minDHSize` {number} Minimum size of the DH parameter in bits to accept a
    TLS connection. When a server offers a DH parameter with a size less
    than `minDHSize`, the TLS connection is destroyed and an error is thrown.
    Defaults to `1024`.
* `callback` {Function}

Creates a new client connection to the given `port` and `host` or
`options.port` and `options.host`. (If `host` is omitted, it defaults to
`localhost`.)

The `callback` function, if specified, will be added as a listener for the
[`'secureConnect'`][] event.

`tls.connect()` returns a [`tls.TLSSocket`][] object.

The following implements a simple "echo server" example:

```js
const tls = require('tls');
const fs = require('fs');

const options = {
  // Necessary only if using the client certificate authentication
  key: fs.readFileSync('client-key.pem'),
  cert: fs.readFileSync('client-cert.pem'),

  // Necessary only if the server uses the self-signed certificate
  ca: [ fs.readFileSync('server-cert.pem') ]
};

const socket = tls.connect(8000, options, () => {
  console.log('client connected',
              socket.authorized ? 'authorized' : 'unauthorized');
  process.stdin.pipe(socket);
  process.stdin.resume();
});
socket.setEncoding('utf8');
socket.on('data', (data) => {
  console.log(data);
});
socket.on('end', () => {
  server.close();
});
```

Or

```js
const tls = require('tls');
const fs = require('fs');

const options = {
  pfx: fs.readFileSync('client.pfx')
};

const socket = tls.connect(8000, options, () => {
  console.log('client connected',
              socket.authorized ? 'authorized' : 'unauthorized');
  process.stdin.pipe(socket);
  process.stdin.resume();
});
socket.setEncoding('utf8');
socket.on('data', (data) => {
  console.log(data);
});
socket.on('end', () => {
  server.close();
});
```


