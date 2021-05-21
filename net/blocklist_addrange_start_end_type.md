<!-- YAML
added: v15.0.0
-->

* `start` {string|net.SocketAddress} The starting IPv4 or IPv6 address in the
  range.
* `end` {string|net.SocketAddress} The ending IPv4 or IPv6 address in the range.
* `type` {string} Either `'ipv4'` or `'ipv6'`. **Default:** `'ipv4'`.

Adds a rule to block a range of IP addresses from `start` (inclusive) to
`end` (inclusive).

