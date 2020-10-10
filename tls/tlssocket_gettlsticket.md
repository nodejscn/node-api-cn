<!-- YAML
added: v0.11.4
-->

* {Buffer}

For a client, returns the TLS session ticket if one is available, or
`undefined`. For a server, always returns `undefined`.

It may be useful for debugging.

See [Session Resumption][] for more information.

