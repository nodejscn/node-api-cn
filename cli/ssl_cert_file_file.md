<!-- YAML
added: v7.7.0
-->

If `--use-openssl-ca` is enabled, this overrides and sets OpenSSL's file
containing trusted certificates.

*Note*: Be aware that unless the child environment is explicitly set, this
evironment variable will be inherited by any child processes, and if they use
OpenSSL, it may cause them to trust the same CAs as node.

