<!-- YAML
added: v12.3.0
-->

* `line` {Buffer} Line of ASCII text, in NSS `SSLKEYLOGFILE` format.

The `keylog` event is emitted on a client `tls.TLSSocket` when key material
is generated or received by the socket. This keying material can be stored
for debugging, as it allows captured TLS traffic to be decrypted. It may
be emitted multiple times, before or after the handshake completes.

A typical use case is to append received lines to a common text file, which
is later used by software (such as Wireshark) to decrypt the traffic:

```js
const logFile = fs.createWriteStream('/tmp/ssl-keys.log', { flags: 'a' });
// ...
tlsSocket.on('keylog', (line) => logFile.write(line));
```

