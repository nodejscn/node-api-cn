<!-- YAML
added: v0.11.3
-->

Emitted after resolving the hostname but before connecting.
Not applicable to UNIX sockets.

* `err` {Error|Null} The error object.  See [`dns.lookup()`][].
* `address` {String} The IP address.
* `family` {String|Null} The address type.  See [`dns.lookup()`][].
* `host` {String} The hostname.

