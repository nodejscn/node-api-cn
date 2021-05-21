<!-- YAML
added: v0.3.2
changes:
  - version: v12.3.0
    pr-url: https://github.com/nodejs/node/pull/27665
    description: The `options` parameter now supports `net.createServer()`
                 options.
  - version: v9.3.0
    pr-url: https://github.com/nodejs/node/pull/14903
    description: The `options` parameter can now include `clientCertEngine`.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11984
    description: The `ALPNProtocols` option can be a `TypedArray` or
     `DataView` now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `options` {Object}
  * `ALPNProtocols`: {string[]|Buffer[]|TypedArray[]|DataView[]|Buffer|
    TypedArray|DataView}
    An array of strings, `Buffer`s or `TypedArray`s or `DataView`s, or a single
    `Buffer` or `TypedArray` or `DataView` containing the supported ALPN
    protocols. `Buffer`s should have the format `[len][name][len][name]...`
    e.g. `0x05hello0x05world`, where the first byte is the length of the next
    protocol name. Passing an array is usually much simpler, e.g.
    `['hello', 'world']`. (Protocols should be ordered by their priority.)
  * `clientCertEngine` {string} Name of an OpenSSL engine which can provide the
    client certificate.
  * `enableTrace` {boolean} If `true`, [`tls.TLSSocket.enableTrace()`][] will be
    called on new connections. Tracing can be enabled after the secure
    connection is established, but this option must be used to trace the secure
    connection setup. **Default:** `false`.
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
  * `SNICallback(servername, callback)` {Function} A function that will be
    called if the client supports SNI TLS extension. Two arguments will be
    passed when called: `servername` and `callback`. `callback` is an
    error-first callback that takes two optional arguments: `error` and `ctx`.
    `ctx`, if provided, is a `SecureContext` instance.
    [`tls.createSecureContext()`][] can be used to get a proper `SecureContext`.
    If `callback` is called with a falsy `ctx` argument, the default secure
    context of the server will be used. If `SNICallback` wasn't provided the
    default callback with high-level API will be used (see below).
  * `ticketKeys`: {Buffer} 48-bytes of cryptographically strong pseudorandom
    data. See [Session Resumption][] for more information.
  * `pskCallback` {Function}
    * socket: {tls.TLSSocket} the server [`tls.TLSSocket`][] instance for
      this connection.
    * identity: {string} identity parameter sent from the client.
    * Returns: {Buffer|TypedArray|DataView} pre-shared key that must either be
      a buffer or `null` to stop the negotiation process. Returned PSK must be
      compatible with the selected cipher's digest.
    When negotiating TLS-PSK (pre-shared keys), this function is called
    with the identity provided by the client.
    If the return value is `null` the negotiation process will stop and an
    "unknown_psk_identity" alert message will be sent to the other party.
    If the server wishes to hide the fact that the PSK identity was not known,
    the callback must provide some random data as `psk` to make the connection
    fail with "decrypt_error" before negotiation is finished.
    PSK ciphers are disabled by default, and using TLS-PSK thus
    requires explicitly specifying a cipher suite with the `ciphers` option.
    More information can be found in the [RFC 4279][].
  * `pskIdentityHint` {string} optional hint to send to a client to help
    with selecting the identity during TLS-PSK negotiation. Will be ignored
    in TLS 1.3. Upon failing to set pskIdentityHint `'tlsClientError'` will be
    emitted with `'ERR_TLS_PSK_SET_IDENTIY_HINT_FAILED'` code.
  * ...: Any [`tls.createSecureContext()`][] option can be provided. For
    servers, the identity options (`pfx`, `key`/`cert` or `pskCallback`)
    are usually required.
  * ...: Any [`net.createServer()`][] option can be provided.
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

