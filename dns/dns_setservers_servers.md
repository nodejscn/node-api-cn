<!-- YAML
added: v0.11.3
-->

Sets the IP addresses of the servers to be used when resolving. The `servers`
argument is an array of IPv4 or IPv6 addresses.

If a port specified on the address it will be removed.

An error will be thrown if an invalid address is provided.

The `dns.setServers()` method must not be called while a DNS query is in
progress.

