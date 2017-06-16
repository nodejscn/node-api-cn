<!-- YAML
added: v0.3.2
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11984
    description: The `ALPNProtocols` and `NPNProtocols` options can
                 be `Uint8Array`s now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `options` {Object}
  * `handshakeTimeout` {number} Abort the connection if the SSL/TLS handshake
    does not finish in the specified number of milliseconds. Defaults to `120`
    seconds. A `'tlsClientError'` is emitted on the `tls.Server` object whenever
    a handshake times out.
  * `requestCert` {boolean} If `true` the server will request a certificate from
    clients that connect and attempt to verify that certificate. Defaults to
    `false`.
  * `rejectUnauthorized` {boolean} If not `false` the server will reject any
    connection which is not authorized with the list of supplied CAs. This
    option only has an effect if `requestCert` is `true`. Defaults to `true`.
  * `NPNProtocols` {string[]|Buffer[]|Uint8Array[]|Buffer|Uint8Array}
    An array of strings, `Buffer`s or `Uint8Array`s, or a single `Buffer` or
    `Uint8Array` containing supported NPN protocols. `Buffer`s should have the
    format `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the
    first byte is the length of the next protocol name. Passing an array is
    usually much simpler, e.g. `['hello', 'world']`.
    (Protocols should be ordered by their priority.)
  * `ALPNProtocols`: {string[]|Buffer[]|Uint8Array[]|Buffer|Uint8Array}
    An array of strings, `Buffer`s or `Uint8Array`s, or a single `Buffer` or
    `Uint8Array` containing the supported ALPN protocols. `Buffer`s should have
    the format `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the
    first byte is the length of the next protocol name. Passing an array is
    usually much simpler, e.g. `['hello', 'world']`.
    (Protocols should be ordered by their priority.)
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
    session tickets on multiple instances of the TLS server.
  * ...: Any [`tls.createSecureContext()`][] options can be provided. For
    servers, the identity options (`pfx` or `key`/`cert`) are usually required.
* `secureConnectionListener` {Function}

Creates a new [tls.Server][].  The `secureConnectionListener`, if provided, is
automatically set as a listener for the [`'secureConnection'`][] event.

*Note*: The `ticketKeys` options is automatically shared between `cluster`
module workers.

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

