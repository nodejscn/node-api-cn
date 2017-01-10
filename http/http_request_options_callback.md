<!-- YAML
added: v0.3.6
-->

* `options` {Object}
  * `protocol` {String} Protocol to use. Defaults to `'http:'`.
  * `host` {String} A domain name or IP address of the server to issue the
    request to. Defaults to `'localhost'`.
  * `hostname` {String} Alias for `host`. To support [`url.parse()`][],
    `hostname` is preferred over `host`.
  * `family` {Number} IP address family to use when resolving `host` and
    `hostname`. Valid values are `4` or `6`. When unspecified, both IP v4 and
    v6 will be used.
  * `port` {Number} Port of remote server. Defaults to 80.
  * `localAddress` {String} Local interface to bind for network connections.
  * `socketPath` {String} Unix Domain Socket (use one of host:port or
    socketPath).
  * `method` {String} A string specifying the HTTP request method. Defaults to
    `'GET'`.
  * `path` {String} Request path. Defaults to `'/'`. Should include query
    string if any. E.G. `'/index.html?page=12'`. An exception is thrown when
    the request path contains illegal characters. Currently, only spaces are
    rejected but that may change in the future.
  * `headers` {Object} An object containing request headers.
  * `auth` {String} Basic authentication i.e. `'user:password'` to compute an
    Authorization header.
  * `agent` {http.Agent|Boolean} Controls [`Agent`][] behavior. When an Agent
    is used request will default to `Connection: keep-alive`. Possible values:
   * `undefined` (default): use [`http.globalAgent`][] for this host and port.
   * `Agent` object: explicitly use the passed in `Agent`.
   * `false`: opts out of connection pooling with an Agent, defaults request to
     `Connection: close`.
  * `createConnection` {Function} A function that produces a socket/stream to
    use for the request when the `agent` option is not used. This can be used to
    avoid creating a custom Agent class just to override the default
    `createConnection` function. See [`agent.createConnection()`][] for more
    details.
  * `timeout` {Integer}: A number specifying the socket timeout in milliseconds.
    This will set the timeout before the socket is connected.
* `callback` {Function}
* Returns: {http.ClientRequest}

Node.js maintains several connections per server to make HTTP requests.
This function allows one to transparently issue requests.

`options` can be an object or a string. If `options` is a string, it is
automatically parsed with [`url.parse()`][].

The optional `callback` parameter will be added as a one time listener for
the [`'response'`][] event.

`http.request()` returns an instance of the [`http.ClientRequest`][]
class. The `ClientRequest` instance is a writable stream. If one needs to
upload a file with a POST request, then write to the `ClientRequest` object.

Example:

```js
var postData = querystring.stringify({
  'msg' : 'Hello World!'
});

var options = {
  hostname: 'www.google.com',
  port: 80,
  path: '/upload',
  method: 'POST',
  headers: {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Content-Length': Buffer.byteLength(postData)
  }
};

var req = http.request(options, (res) => {
  console.log(`STATUS: ${res.statusCode}`);
  console.log(`HEADERS: ${JSON.stringify(res.headers)}`);
  res.setEncoding('utf8');
  res.on('data', (chunk) => {
    console.log(`BODY: ${chunk}`);
  });
  res.on('end', () => {
    console.log('No more data in response.');
  });
});

req.on('error', (e) => {
  console.log(`problem with request: ${e.message}`);
});

// write data to request body
req.write(postData);
req.end();
```

Note that in the example `req.end()` was called. With `http.request()` one
must always call `req.end()` to signify that you're done with the request -
even if there is no data being written to the request body.

If any error is encountered during the request (be that with DNS resolution,
TCP level errors, or actual HTTP parse errors) an `'error'` event is emitted
on the returned request object. As with all `'error'` events, if no listeners
are registered the error will be thrown.

There are a few special headers that should be noted.

* Sending a 'Connection: keep-alive' will notify Node.js that the connection to
  the server should be persisted until the next request.

* Sending a 'Content-length' header will disable the default chunked encoding.

* Sending an 'Expect' header will immediately send the request headers.
  Usually, when sending 'Expect: 100-continue', you should both set a timeout
  and listen for the `'continue'` event. See RFC2616 Section 8.2.3 for more
  information.

* Sending an Authorization header will override using the `auth` option
  to compute basic authentication.

[`'checkContinue'`]: #http_event_checkcontinue
[`'listening'`]: net.html#net_event_listening
[`'request'`]: #http_event_request
[`'response'`]: #http_event_response
[`Agent`]: #http_class_http_agent
[`agent.createConnection()`]: #http_agent_createconnection_options_callback
[`destroy()`]: #http_agent_destroy
[`EventEmitter`]: events.html#events_class_eventemitter
[`http.Agent`]: #http_class_http_agent
[`http.ClientRequest`]: #http_class_http_clientrequest
[`http.globalAgent`]: #http_http_globalagent
[`http.IncomingMessage`]: #http_class_http_incomingmessage
[`http.request()`]: #http_http_request_options_callback
[`http.Server`]: #http_class_http_server
[`message.headers`]: #http_message_headers
[`net.createConnection()`]: net.html#net_net_createconnection_options_connectlistener
[`net.Server`]: net.html#net_class_net_server
[`net.Server.close()`]: net.html#net_server_close_callback
[`net.Server.listen()`]: net.html#net_server_listen_handle_backlog_callback
[`net.Server.listen(path)`]: net.html#net_server_listen_path_backlog_callback
[`net.Server.listen(port)`]: net.html#net_server_listen_port_hostname_backlog_callback
[`net.Socket`]: net.html#net_class_net_socket
[`request.socket.getPeerCertificate()`]: tls.html#tls_tlssocket_getpeercertificate_detailed
[`response.end()`]: #http_response_end_data_encoding_callback
[`response.setHeader()`]: #http_response_setheader_name_value
[`response.write()`]: #http_response_write_chunk_encoding_callback
[`response.write(data, encoding)`]: #http_response_write_chunk_encoding_callback
[`response.writeContinue()`]: #http_response_writecontinue
[`response.writeHead()`]: #http_response_writehead_statuscode_statusmessage_headers
[`socket.setKeepAlive()`]: net.html#net_socket_setkeepalive_enable_initialdelay
[`socket.setNoDelay()`]: net.html#net_socket_setnodelay_nodelay
[`socket.setTimeout()`]: net.html#net_socket_settimeout_timeout_callback
[`TypeError`]: errors.html#errors_class_typeerror
[`url.parse()`]: url.html#url_url_parse_urlstring_parsequerystring_slashesdenotehost
[constructor options]: #http_new_agent_options
[Readable Stream]: stream.html#stream_class_stream_readable
[Writable Stream]: stream.html#stream_class_stream_writable
