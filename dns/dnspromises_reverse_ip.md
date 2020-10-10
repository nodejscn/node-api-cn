<!-- YAML
added: v10.6.0
-->

* `ip` {string}

Performs a reverse DNS query that resolves an IPv4 or IPv6 address to an
array of host names.

On error, the `Promise` is rejected with an [`Error`][] object, where `err.code`
is one of the [DNS error codes](#dns_error_codes).

