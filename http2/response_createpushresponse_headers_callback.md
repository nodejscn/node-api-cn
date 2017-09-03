<!-- YAML
added: v8.4.0
-->

Call [`stream.pushStream()`][] with the given headers, and wraps the
given newly created [`Http2Stream`] on `Http2ServerRespose`.

The callback will be called with an error with code `ERR_HTTP2_STREAM_CLOSED`
if the stream is closed.

[HTTP/2]: https://tools.ietf.org/html/rfc7540
[HTTP/1]: http.html
[HTTPS]: https.html
[`net.Socket`]: net.html
[`tls.TLSSocket`]: tls.html
[`tls.createServer()`]: tls.html#tls_tls_createserver_options_secureconnectionlistener
[`ClientHttp2Stream`]: #http2_class_clienthttp2stream
[Compatibility API]: #http2_compatibility_api
[ALPN negotiation]: #http2_alpn_negotiation
[`Duplex`]: stream.html#stream_class_stream_duplex
[Headers Object]: #http2_headers_object
[`Http2Stream`]: #http2_class_http2stream
[Http2Session and Sockets]: #http2_http2sesion_and_sockets
[`ServerHttp2Stream`]: #http2_class_serverhttp2stream
[Settings Object]: #http2_settings_object
[Using options.selectPadding]: #http2_using_options_selectpadding
[error code]: #error_codes
[`'unknownProtocol'`]: #http2_event_unknownprotocol
[`'request'`]: #http2_event_request
[Readable Stream]: stream.html#stream_class_stream_readable
[`ServerRequest`]: #http2_class_server_request
[`stream.pushStream()`]: #http2_stream-pushstream
