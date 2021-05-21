<!-- YAML
added: v15.0.0
-->

* `net` {string|net.SocketAddress} The network IPv4 or IPv6 address.
* `prefix` {number} The number of CIDR prefix bits. For IPv4, this
  must be a value between `0` and `32`. For IPv6, this must be between
  `0` and `128`.
* `type` {string} Either `'ipv4'` or `'ipv6'`. **Default:** `'ipv4'`.

Adds a rule to block a range of IP addresses specified as a subnet mask.

