<!-- YAML
added: v8.4.0
-->

Call [`http2stream.pushStream()`][] with the given headers, and wraps the
given newly created [`Http2Stream`] on `Http2ServerRespose`.

The callback will be called with an error with code `ERR_HTTP2_STREAM_CLOSED`
if the stream is closed.

[ALPN negotiation]: #http2_alpn_negotiation
[Compatibility API]: #http2_compatibility_api
[HTTP/1]: http.html
[HTTP/2]: https://tools.ietf.org/html/rfc7540
[HTTPS]: https.html
[Headers Object]: #http2_headers_object
[Http2Session and Sockets]: #http2_http2session_and_sockets
[Readable Stream]: stream.html#stream_class_stream_readable
[Settings Object]: #http2_settings_object
[Using options.selectPadding]: #http2_using_options_selectpadding
[Writable Stream]: stream.html#stream_writable_streams
[`'checkContinue'`]: #http2_event_checkcontinue
[`'request'`]: #http2_event_request
[`'unknownProtocol'`]: #http2_event_unknownprotocol
[`ClientHttp2Stream`]: #http2_class_clienthttp2stream
[`Duplex`]: stream.html#stream_class_stream_duplex
[`EventEmitter`]: events.html#events_class_eventemitter
[`Http2ServerRequest`]: #http2_class_http2_http2serverrequest
[`Http2Stream`]: #http2_class_http2stream
[`ServerHttp2Stream`]: #http2_class_serverhttp2stream
[`TypeError`]: errors.html#errors_class_typeerror
[`http2.SecureServer`]: #http2_class_http2secureserver
[`http2.createSecureServer()`]: #http2_http2_createsecureserver_options_onrequesthandler
[`http2.Server`]: #http2_class_http2server
[`http2.createServer()`]: #http2_http2_createserver_options_onrequesthandler
[`http2stream.pushStream()`]: #http2_http2stream_pushstream_headers_options_callback
[`net.Socket`]: net.html#net_class_net_socket
[`net.connect()`]: net.html#net_net_connect
[`request.socket.getPeerCertificate()`]: tls.html#tls_tlssocket_getpeercertificate_detailed
[`response.end()`]: #http2_response_end_data_encoding_callback
[`response.setHeader()`]: #http2_response_setheader_name_value
[`response.socket`]: #http2_response_socket
[`response.write()`]: #http2_response_write_chunk_encoding_callback
[`response.write(data, encoding)`]: http.html#http_response_write_chunk_encoding_callback
[`response.writeContinue()`]: #http2_response_writecontinue
[`response.writeHead()`]: #http2_response_writehead_statuscode_statusmessage_headers
[`tls.TLSSocket`]: tls.html#tls_class_tls_tlssocket
[`tls.connect()`]: tls.html#tls_tls_connect_options_callback
[`tls.createServer()`]: tls.html#tls_tls_createserver_options_secureconnectionlistener
[error code]: #error_codes
