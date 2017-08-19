
Every `Http2Session` instance is associated with exactly one [`net.Socket`][] or
[`tls.TLSSocket`][] when it is created. When either the `Socket` or the
`Http2Session` are destroyed, both will be destroyed.

Because the of the specific serialization and processing requirements imposed
by the HTTP/2 protocol, it is not recommended for user code to read data from
or write data to a `Socket` instance bound to a `Http2Session`. Doing so can
put the HTTP/2 session into an indeterminate state causing the session and
the socket to become unusable.

Once a `Socket` has been bound to an `Http2Session`, user code should rely
solely on the API of the `Http2Session`.

