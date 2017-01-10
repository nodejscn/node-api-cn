<!-- YAML
added: v0.1.17
-->

An `IncomingMessage` object is created by [`http.Server`][] or
[`http.ClientRequest`][] and passed as the first argument to the [`'request'`][]
and [`'response'`][] event respectively. It may be used to access response status,
headers and data.

It implements the [Readable Stream][] interface, as well as the
following additional events, methods, and properties.

