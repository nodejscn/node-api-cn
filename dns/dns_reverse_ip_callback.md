<!-- YAML
added: v0.1.16
-->
- `ip` {string}
- `callback` {Function}
  - `err` {Error}
  - `hostnames` {string[]}

Performs a reverse DNS query that resolves an IPv4 or IPv6 address to an
array of hostnames.

On error, `err` is an [`Error`][] object, where `err.code` is
one of the [DNS error codes][].

