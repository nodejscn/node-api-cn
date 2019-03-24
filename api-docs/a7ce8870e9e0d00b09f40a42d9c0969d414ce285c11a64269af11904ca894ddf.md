<!-- YAML
added: v6.11.0
-->

Use bundled Mozilla CA store as supplied by current Node.js version
or use OpenSSL's default CA store. The default store is selectable
at build-time.

The bundled CA store, as supplied by Node.js, is a snapshot of Mozilla CA store
that is fixed at release time. It is identical on all supported platforms.

Using OpenSSL store allows for external modifications of the store. For most
Linux and BSD distributions, this store is maintained by the distribution
maintainers and system administrators. OpenSSL CA store location is dependent on
configuration of the OpenSSL library but this can be altered at runtime using
environment variables.

See `SSL_CERT_DIR` and `SSL_CERT_FILE`.

