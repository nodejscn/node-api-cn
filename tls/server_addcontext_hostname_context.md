<!-- YAML
added: v0.5.3
-->

* `hostname` {string} A SNI hostname or wildcard (e.g. `'*'`)
* `context` {Object} An object containing any of the possible properties
  from the [`tls.createSecureContext()`][] `options` arguments (e.g. `key`,
  `cert`, `ca`, etc).

The `server.addContext()` method adds a secure context that will be used if
the client request's SNI hostname matches the supplied `hostname` (or wildcard).

