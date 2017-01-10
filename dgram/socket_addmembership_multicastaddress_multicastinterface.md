<!-- YAML
added: v0.6.9
-->

* `multicastAddress` {String}
* `multicastInterface` {String}, Optional

Tells the kernel to join a multicast group at the given `multicastAddress` and
`multicastInterface` using the `IP_ADD_MEMBERSHIP` socket option. If the
`multicastInterface` argument is not specified, the operating system will choose
one interface and will add membership to it. To add membership to every
available interface, call `addMembership` multiple times, once per interface.

