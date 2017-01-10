<!-- YAML
added: v0.1.16
-->

Performs a reverse DNS query that resolves an IPv4 or IPv6 address to an
array of hostnames.

The `callback` function has arguments `(err, hostnames)`, where `hostnames`
is an array of resolved hostnames for the given `ip`.

On error, `err` is an [`Error`][] object, where `err.code` is
one of the [DNS error codes][].

