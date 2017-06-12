<!-- YAML
added: v0.11.3
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12839
    description: The `lookup` option is supported now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11984
    description: The `ALPNProtocols` and `NPNProtocols` options can
                 be `Uint8Array`s now.
  - version: v5.3.0, v4.7.0
    pr-url: https://github.com/nodejs/node/pull/4246
    description: The `secureContext` option is supported now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `options` {Object}
  * `host` {string} Host the client should connect to, defaults to 'localhost'.
  * `port` {number} Port the client should connect to.
  * `path` {string} Creates unix socket connection to path. If this option is
    specified, `host` and `port` are ignored.
  * `socket` {net.Socket} Establish secure connection on a given socket rather
    than creating a new socket. If this option is specified, `path`, `host` and
    `port` are ignored.  Usually, a socket is already connected when passed to
    `tls.connect()`, but it can be connected later. Note that
    connection/disconnection/destruction of `socket` is the user's
    responsibility, calling `tls.connect()` will not cause `net.connect()` to be
    called.
  * `rejectUnauthorized` {boolean} If not `false`, the server certificate is verified
    against the list of supplied CAs. An `'error'` event is emitted if
    verification fails; `err.code` contains the OpenSSL error code. Defaults to
    `true`.
  * `NPNProtocols` {string[]|Buffer[]|Uint8Array[]|Buffer|Uint8Array}
    An array of strings, `Buffer`s or `Uint8Array`s, or a single `Buffer` or
    `Uint8Array` containing supported NPN protocols. `Buffer`s should have the
    format `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the
    first byte is the length of the next protocol name. Passing an array is
    usually much simpler, e.g. `['hello', 'world']`.
  * `ALPNProtocols`: {string[]|Buffer[]|Uint8Array[]|Buffer|Uint8Array}
    An array of strings, `Buffer`s or `Uint8Array`s, or a single `Buffer` or
    `Uint8Array` containing the supported ALPN protocols. `Buffer`s should have
    the format `[len][name][len][name]...` e.g. `0x05hello0x05world`, where the
    first byte is the length of the next protocol name. Passing an array is
    usually much simpler, e.g. `['hello', 'world']`.
  * `servername`: {string} Server name for the SNI (Server Name Indication) TLS
    extension.
  * `checkServerIdentity(servername, cert)` {Function} A callback function
    to be used when checking the server's hostname against the certificate.
    This should throw an error if verification fails. The method should return
    `undefined` if the `servername` and `cert` are verified.
  * `session` {Buffer} A `Buffer` instance, containing TLS session.
  * `minDHSize` {number} Minimum size of the DH parameter in bits to accept a
    TLS connection. When a server offers a DH parameter with a size less
    than `minDHSize`, the TLS connection is destroyed and an error is thrown.
    Defaults to `1024`.
  * `secureContext`: Optional TLS context object created with
    [`tls.createSecureContext()`][]. If a `secureContext` is _not_ provided, one
    will be created by passing the entire `options` object to
    `tls.createSecureContext()`.
  * `lookup`: {Function} Custom lookup function. Defaults to [`dns.lookup()`][].
  * ...: Optional [`tls.createSecureContext()`][] options that are used if the
    `secureContext` option is missing, otherwise they are ignored.
* `callback` {Function}

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

