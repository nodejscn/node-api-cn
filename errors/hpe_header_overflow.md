
Too much HTTP header data was received. In order to protect against malicious or
malconfigured clients, if more than 80KB of HTTP header data is received then
HTTP parsing will abort without a request or response object being created, and
an `Error` with this code will be emitted.

<a id="MODULE_NOT_FOUND"></a>
