
The [Performance Observer][] API can be used to collect basic performance
metrics for each `Http2Session` and `Http2Stream` instance.

```js
const { PerformanceObserver } = require('perf_hooks');

const obs = new PerformanceObserver((items) => {
  const entry = items.getEntries()[0];
  console.log(entry.entryType);  // prints 'http2'
  if (entry.name === 'Http2Session') {
    // entry contains statistics about the Http2Session
  } else if (entry.name === 'Http2Stream') {
    // entry contains statistics about the Http2Stream
  }
});
obs.observe({ entryTypes: ['http2'] });
```

The `entryType` property of the `PerformanceEntry` will be equal to `'http2'`.

The `name` property of the `PerformanceEntry` will be equal to either
`'Http2Stream'` or `'Http2Session'`.

If `name` is equal to `Http2Stream`, the `PerformanceEntry` will contain the
following additional properties:

* `bytesRead` {number} The number of `DATA` frame bytes received for this
  `Http2Stream`.
* `bytesWritten` {number} The number of `DATA` frame bytes sent for this
  `Http2Stream`.
* `id` {number} The identifier of the associated `Http2Stream`
* `timeToFirstByte` {number} The number of milliseconds elapsed between the
  `PerformanceEntry` `startTime` and the reception of the first `DATA` frame.
* `timeToFirstByteSent` {number} The number of milliseconds elapsed between
  the `PerformanceEntry` `startTime` and sending of the first `DATA` frame.
* `timeToFirstHeader` {number} The number of milliseconds elapsed between the
  `PerformanceEntry` `startTime` and the reception of the first header.

If `name` is equal to `Http2Session`, the `PerformanceEntry` will contain the
following additional properties:

* `bytesRead` {number} The number of bytes received for this `Http2Session`.
* `bytesWritten` {number} The number of bytes sent for this `Http2Session`.
* `framesReceived` {number} The number of HTTP/2 frames received by the
  `Http2Session`.
* `framesSent` {number} The number of HTTP/2 frames sent by the `Http2Session`.
* `maxConcurrentStreams` {number} The maximum number of streams concurrently
  open during the lifetime of the `Http2Session`.
* `pingRTT` {number} The number of milliseconds elapsed since the transmission
  of a `PING` frame and the reception of its acknowledgment. Only present if
  a `PING` frame has been sent on the `Http2Session`.
* `streamAverageDuration` {number} The average duration (in milliseconds) for
  all `Http2Stream` instances.
* `streamCount` {number} The number of `Http2Stream` instances processed by
  the `Http2Session`.
* `type` {string} Either `'server'` or `'client'` to identify the type of
  `Http2Session`.

[ALPN negotiation]: #http2_alpn_negotiation
[ALPN Protocol ID]: https://www.iana.org/assignments/tls-extensiontype-values/tls-extensiontype-values.xhtml#alpn-protocol-ids
[Compatibility API]: #http2_compatibility_api
[HTTP/1]: http.html
[HTTP/2]: https://tools.ietf.org/html/rfc7540
[HTTP/2 Unencrypted]: https://http2.github.io/faq/#does-http2-require-encryption
[HTTP/2 Headers Object]: #http2_headers_object
[HTTP/2 Settings Object]: #http2_settings_object
[HTTPS]: https.html
[Performance Observer]: perf_hooks.html
[Readable Stream]: stream.html#stream_class_stream_readable
[RFC 7838]: https://tools.ietf.org/html/rfc7838
[Using `options.selectPadding()`]: #http2_using_options_selectpadding
[Writable Stream]: stream.html#stream_writable_streams
[`'checkContinue'`]: #http2_event_checkcontinue
[`'request'`]: #http2_event_request
[`'unknownProtocol'`]: #http2_event_unknownprotocol
[`ClientHttp2Stream`]: #http2_class_clienthttp2stream
[`Duplex`]: stream.html#stream_class_stream_duplex
[`EventEmitter`]: events.html#events_class_eventemitter
[`Http2ServerRequest`]: #http2_class_http2_http2serverrequest
[`Http2Session` and Sockets]: #http2_http2session_and_sockets
[`Http2Stream`]: #http2_class_http2stream
[`ServerHttp2Stream`]: #http2_class_serverhttp2stream
[`TypeError`]: errors.html#errors_class_typeerror
[`http2.SecureServer`]: #http2_class_http2secureserver
[`http2.createSecureServer()`]: #http2_http2_createsecureserver_options_onrequesthandler
[`http2.Server`]: #http2_class_http2server
[`http2.createServer()`]: #http2_http2_createserver_options_onrequesthandler
[`http2session.close()`]: #http2_http2session_close_callback
[`http2stream.pushStream()`]: #http2_http2stream_pushstream_headers_options_callback
[`net.Server.close()`]: net.html#net_server_close_callback
[`net.Socket`]: net.html#net_class_net_socket
[`net.Socket.prototype.ref()`]: net.html#net_socket_ref
[`net.Socket.prototype.unref()`]: net.html#net_socket_unref
[`net.connect()`]: net.html#net_net_connect
[`request.socket.getPeerCertificate()`]: tls.html#tls_tlssocket_getpeercertificate_detailed
[`response.end()`]: #http2_response_end_data_encoding_callback
[`response.setHeader()`]: #http2_response_setheader_name_value
[`response.socket`]: #http2_response_socket
[`response.write()`]: #http2_response_write_chunk_encoding_callback
[`response.write(data, encoding)`]: http.html#http_response_write_chunk_encoding_callback
[`response.writeContinue()`]: #http2_response_writecontinue
[`response.writeHead()`]: #http2_response_writehead_statuscode_statusmessage_headers
[`tls.Server.close()`]: tls.html#tls_server_close_callback
[`tls.TLSSocket`]: tls.html#tls_class_tls_tlssocket
[`tls.connect()`]: tls.html#tls_tls_connect_options_callback
[`tls.createServer()`]: tls.html#tls_tls_createserver_options_secureconnectionlistener
[error code]: #error_codes
