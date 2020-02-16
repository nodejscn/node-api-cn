<!-- YAML
added: v0.11.3
changes:
  - version: v12.16.0
    pr-url: https://github.com/nodejs/node/pull/23188
    description: The `pskCallback` option is now supported.
  - version: v12.9.0
    pr-url: https://github.com/nodejs/node/pull/27836
    description: Support the `allowHalfOpen` option.
  - version: v12.4.0
    pr-url: https://github.com/nodejs/node/pull/27816
    description: The `hints` option is now supported.
  - version: v12.2.0
    pr-url: https://github.com/nodejs/node/pull/27497
    description: The `enableTrace` option is now supported.
  - version: v11.8.0
    pr-url: https://github.com/nodejs/node/pull/25517
    description: The `timeout` option is supported now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/12839
    description: The `lookup` option is supported now.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11984
    description: The `ALPNProtocols` option can be a `TypedArray` or
     `DataView` now.
  - version: v5.3.0, v4.7.0
    pr-url: https://github.com/nodejs/node/pull/4246
    description: The `secureContext` option is supported now.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/2564
    description: ALPN options are supported now.
-->

* `options` {Object}
  * `enableTrace`: See [`tls.createServer()`][]
  * `host` {string} Host the client should connect to. **Default:**
    `'localhost'`.
  * `port` {number} Port the client should connect to.
  * `path` {string} Creates Unix socket connection to path. If this option is
    specified, `host` and `port` are ignored.
  * `socket` {stream.Duplex} Establish secure connection on a given socket
    rather than creating a new socket. Typically, this is an instance of
    [`net.Socket`][], but any `Duplex` stream is allowed.
    If this option is specified, `path`, `host` and `port` are ignored,
    except for certificate validation. Usually, a socket is already connected
    when passed to `tls.connect()`, but it can be connected later.
    Connection/disconnection/destruction of `socket` is the user's
    responsibility; calling `tls.connect()` will not cause `net.connect()` to be
    called.
  * `allowHalfOpen` {boolean} If the `socket` option is missing, indicates
    whether or not to allow the internally created socket to be half-open,
    otherwise the option is ignored. See the `allowHalfOpen` option of
    [`net.Socket`][] for details. **Default:** `false`.
  * `rejectUnauthorized` {boolean} If not `false`, the server certificate is
    verified against the list of supplied CAs. An `'error'` event is emitted if
    verification fails; `err.code` contains the OpenSSL error code. **Default:**
    `true`.
  * `pskCallback` {Function}
    * hint: {string} optional message sent from the server to help client
      decide which identity to use during negotiation.
      Always `null` if TLS 1.3 is used.
    * Returns: {Object} in the form
      `{ psk: <Buffer|TypedArray|DataView>, identity: <string> }`
      or `null` to stop the negotiation process. `psk` must be
      compatible with the selected cipher's digest.
      `identity` must use UTF-8 encoding.
    When negotiating TLS-PSK (pre-shared keys), this function is called
    with optional identity `hint` provided by the server or `null`
    in case of TLS 1.3 where `hint` was removed.
    It will be necessary to provide a custom `tls.checkServerIdentity()`
    for the connection as the default one will try to check hostname/IP
    of the server against the certificate but that's not applicable for PSK
    because there won't be a certificate present.
    More information can be found in the [RFC 4279][].
  * `ALPNProtocols`: {string[]|Buffer[]|TypedArray[]|DataView[]|Buffer|
    TypedArray|DataView}
    An array of strings, `Buffer`s or `TypedArray`s or `DataView`s, or a
    single `Buffer` or `TypedArray` or `DataView` containing the supported ALPN
    protocols. `Buffer`s should have the format `[len][name][len][name]...`
    e.g. `'\x08http/1.1\x08http/1.0'`, where the `len` byte is the length of the
    next protocol name. Passing an array is usually much simpler, e.g.
    `['http/1.1', 'http/1.0']`. Protocols earlier in the list have higher
    preference than those later.
  * `servername`: {string} Server name for the SNI (Server Name Indication) TLS
    extension. It is the name of the host being connected to, and must be a host
    name, and not an IP address. It can be used by a multi-homed server to
    choose the correct certificate to present to the client, see the
    `SNICallback` option to [`tls.createServer()`][].
  * `checkServerIdentity(servername, cert)` {Function} A callback function
    to be used (instead of the builtin `tls.checkServerIdentity()` function)
    when checking the server's hostname (or the provided `servername` when
    explicitly set) against the certificate. This should return an {Error} if
    verification fails. The method should return `undefined` if the `servername`
    and `cert` are verified.
  * `session` {Buffer} A `Buffer` instance, containing TLS session.
  * `minDHSize` {number} Minimum size of the DH parameter in bits to accept a
    TLS connection. When a server offers a DH parameter with a size less
    than `minDHSize`, the TLS connection is destroyed and an error is thrown.
    **Default:** `1024`.
  * `secureContext`: TLS context object created with
    [`tls.createSecureContext()`][]. If a `secureContext` is _not_ provided, one
    will be created by passing the entire `options` object to
    `tls.createSecureContext()`.
  * ...: [`tls.createSecureContext()`][] options that are used if the
    `secureContext` option is missing, otherwise they are ignored.
  * ...: Any [`socket.connect()`][] option not already listed.
* `callback` {Function}
* Returns: {tls.TLSSocket}

The `callback` function, if specified, will be added as a listener for the
[`'secureConnect'`][] event.

`tls.connect()` returns a [`tls.TLSSocket`][] object.

The following illustrates a client for the echo server example from


```js
// Assumes an echo server that is listening on port 8000.
const tls = require('tls');
const fs = require('fs');

const options = {
  // Necessary only if the server requires client certificate authentication.
  key: fs.readFileSync('client-key.pem'),
  cert: fs.readFileSync('client-cert.pem'),

  // Necessary only if the server uses a self-signed certificate.
  ca: [ fs.readFileSync('server-cert.pem') ],

  // Necessary only if the server's cert isn't for "localhost".
  checkServerIdentity: () => { return null; },
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
  console.log('server ends connection');
});
```

