<!-- YAML
added: v8.6.0
-->

* `multicastInterface` {String}

*Note: All references to scope in this section are refering to
[IPv6 Zone Indices][], which are defined by [RFC 4007][]. In string form, an IP
with a scope index is written as `'IP%scope'` where scope is an interface name or
interface number.*

Sets the default outgoing multicast interface of the socket to a chosen
interface or back to system interface selection. The `multicastInterface` must
be a valid string representation of an IP from the socket's family.

For IPv4 sockets, this should be the IP configured for the desired physical
interface. All packets sent to multicast on the socket will be sent on the
interface determined by the most recent successful use of this call.

For IPv6 sockets, `multicastInterface` should include a scope to indicate the
interface as in the examples that follow. In IPv6, individual `send` calls can
also use explicit scope in addresses, so only packets sent to a multicast
address without specifying an explicit scope are affected by the most recent
successful use of this call.

