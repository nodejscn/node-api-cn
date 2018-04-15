<!-- YAML
added: v0.11.4
-->

Returns an object representing the cipher name. The `version` key is a legacy
field which always contains the value `'TLSv1/SSLv3'`.

For example: `{ name: 'AES256-SHA', version: 'TLSv1/SSLv3' }`

See `SSL_CIPHER_get_name()` in
https://www.openssl.org/docs/man1.0.2/ssl/SSL_CIPHER_get_name.html for more
information.
