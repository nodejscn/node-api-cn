
HTTP/2 Informational headers must only be sent *prior* to calling the
`Http2Stream.prototype.respond()` method.

<a id="ERR_HTTP2_INFO_STATUS_NOT_ALLOWED"></a>
