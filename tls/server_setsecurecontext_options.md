<!-- YAML
added: v11.0.0
-->

* `options` {Object} An object containing any of the possible properties from
  the [`tls.createSecureContext()`][] `options` arguments (e.g. `key`, `cert`,
  `ca`, etc).

The `server.setSecureContext()` method replaces the secure context of an
existing server. Existing connections to the server are not interrupted.

