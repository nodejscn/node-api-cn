<!-- YAML
added: v0.3.2
changes:
  - version: v9.3.0
    pr-url: https://github.com/nodejs/node/pull/14903
    description: The `options` parameter can now include `clientCertEngine`.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11984
    description: The `ALPNProtocols` option can be a `Uint8Array` now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `options` {Object}
  * `ALPNProtocols`: {string[]|Buffer[]|Uint8Array[]|Buffer|Uint8Array}
    An array of strings, `Buffer`s or `Uint8Array`s, or a single `Buffer` or
    `Uint8Array` containing the supported ALPN protocols. `Buffer`s should have
    the format `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the
    first byte is the length of the next protocol name. Passing an array is
    usually much simpler, e.g. `['hello', 'world']`.
    (Protocols should be ordered by their priority.)
  * `clientCertEngine` {string} Name of an OpenSSL engine which can provide the
    client certificate.
  * `handshakeTimeout` {number} Abort the connection if the SSL/TLS handshake
    does not finish in the specified number of milliseconds.
    A `'tlsClientError'` is emitted on the `tls.Server` object whenever
    a handshake times out. **Default:** `120000` (120 seconds).
  * `rejectUnauthorized` {boolean} If not `false` the server will reject any
    connection which is not authorized with the list of supplied CAs. This
    option only has an effect if `requestCert` is `true`. **Default:** `true`.
  * `requestCert` {boolean} If `true` the server will request a certificate from
    clients that connect and attempt to verify that certificate. **Default:**
    `false`.
  * `sessionTimeout` {number} The number of seconds after which a TLS session
    created by the server will no longer be resumable. See
    [Session Resumption][] for more information. **Default:** `300`.
  * `SNICallback(servername, cb)` {Function} A function that will be called if
    the client supports SNI TLS extension. Two arguments will be passed when
    called: `servername` and `cb`. `SNICallback` should invoke `cb(null, ctx)`,
    where `ctx` is a `SecureContext` instance. (`tls.createSecureContext(...)`
    can be used to get a proper `SecureContext`.) If `SNICallback` wasn't
    provided the default callback with high-level API will be used (see below).
  * `ticketKeys`: {Buffer} 48-bytes of cryptographically strong pseudo-random
    data. See [Session Resumption][] for more information.
  * ...: Any [`tls.createSecureContext()`][] option can be provided. For
    servers, the identity options (`pfx` or `key`/`cert`) are usually required.
* `secureConnectionListener` {Function}
* Returns: {tls.Server}

Creates a new [`tls.Server`][]. The `secureConnectionListener`, if provided, is
automatically set as a listener for the [`'secureConnection'`][] event.

The `ticketKeys` options is automatically shared between `cluster` module
workers.

The following illustrates a simple echo server:

```js
const tls = require('tls');
const fs = require('fs');

const options = {
  key: fs.readFileSync('server-key.pem'),
  cert: fs.readFileSync('server-cert.pem'),

  // This is necessary only if using client certificate authentication.
  requestCert: true,

  // This is necessary only if the client uses a self-signed certificate.
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

The server can be tested by connecting to it using the example client from
[`tls.connect()`][].

