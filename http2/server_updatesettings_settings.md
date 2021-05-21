<!-- YAML
added: v15.1.0
-->

* `settings` {HTTP/2 Settings Object}

Used to update the server with the provided settings.

Throws `ERR_HTTP2_INVALID_SETTING_VALUE` for invalid `settings` values.

Throws `ERR_INVALID_ARG_TYPE` for invalid `settings` argument.

