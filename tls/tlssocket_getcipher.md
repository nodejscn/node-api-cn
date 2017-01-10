<!-- YAML
added: v0.11.4
-->

Returns an object representing the cipher name and the SSL/TLS protocol version
that first defined the cipher.

For example: `{ name: 'AES256-SHA', version: 'TLSv1/SSLv3' }`

See `SSL_CIPHER_get_name()` and `SSL_CIPHER_get_version()` in
https://www.openssl.org/docs/man1.0.2/ssl/SSL_CIPHER_get_name.html for more
information.

