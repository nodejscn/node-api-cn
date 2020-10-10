
The format of the `alt` parameter is strictly defined by [RFC 7838][] as an
ASCII string containing a comma-delimited list of "alternative" protocols
associated with a specific host and port.

For example, the value `'h2="example.org:81"'` indicates that the HTTP/2
protocol is available on the host `'example.org'` on TCP/IP port 81. The
host and port *must* be contained within the quote (`"`) characters.

Multiple alternatives may be specified, for instance: `'h2="example.org:81",
h2=":82"'`.

The protocol identifier (`'h2'` in the examples) may be any valid
[ALPN Protocol ID][].

The syntax of these values is not validated by the Node.js implementation and
are passed through as provided by the user or received from the peer.

