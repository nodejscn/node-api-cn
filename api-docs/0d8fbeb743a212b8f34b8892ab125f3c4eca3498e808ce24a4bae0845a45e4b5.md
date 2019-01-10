<!-- YAML
added: v3.0.0
-->

* `keys` {Buffer} The keys used for encryption/decryption of the
  [TLS Session Tickets][].

Updates the keys for encryption/decryption of the [TLS Session Tickets][].

The key's `Buffer` should be 48 bytes long. See `ticketKeys` option in
[`tls.createServer()`] for more information on how it is used.

Changes to the ticket keys are effective only for future server connections.
Existing or currently pending server connections will use the previous keys.

