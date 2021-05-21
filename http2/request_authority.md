<!-- YAML
added: v8.4.0
-->

* {string}

The request authority pseudo header field. Because HTTP/2 allows requests
to set either `:authority` or `host`, this value is derived from
`req.headers[':authority']` if present. Otherwise, it is derived from
`req.headers['host']`.

