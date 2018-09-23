<!-- YAML
changes:
  - version: v9.2.0
    pr-url: https://github.com/nodejs/node/pull/16130
    description: Runtime deprecation.
-->

Type: Runtime

The `ecdhCurve` option to `tls.createSecureContext()` and `tls.TLSSocket` could
be set to `false` to disable ECDH entirely on the server only. This mode is
deprecated in preparation for migrating to OpenSSL 1.1.0 and consistency with
the client. Use the `ciphers` parameter instead.

<a id="DEP0084"></a>
