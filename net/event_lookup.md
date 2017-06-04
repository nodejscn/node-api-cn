<!-- YAML
added: v0.11.3
changes:
  - version: v5.10.0
    pr-url: https://github.com/nodejs/node/pull/5598
    description: The `host` parameter is supported now.
-->

Emitted after resolving the hostname but before connecting.
Not applicable to UNIX sockets.

* `err` {Error|null} The error object.  See [`dns.lookup()`][].
* `address` {string} The IP address.
* `family` {string|null} The address type.  See [`dns.lookup()`][].
* `host` {string} The hostname.

