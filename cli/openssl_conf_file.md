<!-- YAML
added: v7.7.0
-->

Load an OpenSSL configuration file on startup. Among other uses, this can be
used to enable FIPS-compliant crypto if Node.js is built with `./configure
--openssl-fips`.

If the [`--openssl-config`][] command line option is used, the environment
variable is ignored.

