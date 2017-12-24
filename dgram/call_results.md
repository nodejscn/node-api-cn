
A call on a socket that is not ready to send or no longer open may throw a *Not
running* [`Error`][].

If `multicastInterface` can not be parsed into an IP then an *EINVAL*
[`System Error`][] is thrown.

On IPv4, if `multicastInterface` is a valid address but does not match any
interface, or if the address does not match the family then
a [`System Error`][] such as `EADDRNOTAVAIL` or `EPROTONOSUP` is thrown.

On IPv6, most errors with specifying or omitting scope will result in the socket
continuing to use (or returning to) the system's default interface selection.

A socket's address family's ANY address (IPv4 `'0.0.0.0'` or IPv6 `'::'`) can be
used to return control of the sockets default outgoing interface to the system
for future multicast packets.


