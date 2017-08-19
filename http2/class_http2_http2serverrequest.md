<!-- YAML
added: v8.4.0
-->

A `Http2ServerRequest` object is created by [`http2.Server`][] or
[`http2.SecureServer`][] and passed as the first argument to the
[`'request'`][] event. It may be used to access a request status, headers and
data.

It implements the [Readable Stream][] interface, as well as the
following additional events, methods, and properties.

