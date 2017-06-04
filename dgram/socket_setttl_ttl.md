<!-- YAML
added: v0.1.101
-->

* `ttl` {number} Integer

Sets the `IP_TTL` socket option. While TTL generally stands for "Time to Live",
in this context it specifies the number of IP hops that a packet is allowed to
travel through.  Each router or gateway that forwards a packet decrements the
TTL.  If the TTL is decremented to 0 by a router, it will not be forwarded.
Changing TTL values is typically done for network probes or when multicasting.

The argument to `socket.setTTL()` is a number of hops between 1 and 255.
The default on most systems is 64 but can vary.

