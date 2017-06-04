<!-- YAML
added: v0.3.8
-->

* `ttl` {number} Integer

Sets the `IP_MULTICAST_TTL` socket option.  While TTL generally stands for
"Time to Live", in this context it specifies the number of IP hops that a
packet is allowed to travel through, specifically for multicast traffic.  Each
router or gateway that forwards a packet decrements the TTL. If the TTL is
decremented to 0 by a router, it will not be forwarded.

The argument passed to to `socket.setMulticastTTL()` is a number of hops
between 0 and 255. The default on most systems is `1` but can vary.

