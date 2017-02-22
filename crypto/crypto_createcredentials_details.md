<!-- YAML
added: v0.1.92
deprecated: v0.11.13
-->

> Stability: 0 - Deprecated: Use [`tls.createSecureContext()`][] instead.

- `details` {Object} Identical to [`tls.createSecureContext()`][].

The `crypto.createCredentials()` method is a deprecated function for creating
and returning a `tls.SecureContext`. It should not be used. Replace it with
[`tls.createSecureContext()`][] which has the exact same arguments and return
value.

Returns a `tls.SecureContext`, as-if [`tls.createSecureContext()`][] had been
called.

