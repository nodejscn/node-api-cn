<!-- YAML
added: v3.0.0
-->

* `keys` {Buffer|TypedArray|DataView} A 48-byte buffer containing the session
  ticket keys.

Sets the session ticket keys.

Changes to the ticket keys are effective only for future server connections.
Existing or currently pending server connections will use the previous keys.

See [Session Resumption][] for more information.

