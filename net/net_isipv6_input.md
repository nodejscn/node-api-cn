<!-- YAML
added: v0.3.0
-->

如果 input 是 IPv6 地址则返回 true，否则返回 false。

[`'close'`]: #net_event_close
[`'connect'`]: #net_event_connect
[`'connection'`]: #net_event_connection
[`'data'`]: #net_event_data
[`'drain'`]: #net_event_drain
[`'end'`]: #net_event_end
[`'error'`]: #net_event_error_1
[`'listening'`]: #net_event_listening
[`'timeout'`]: #net_event_timeout
[`EventEmitter`]: events.html#events_class_eventemitter
[`child_process.fork()`]: child_process.html#child_process_child_process_fork_modulepath_args_options
[`dns.lookup()` hints]: dns.html#dns_supported_getaddrinfo_flags
[`dns.lookup()`]: dns.html#dns_dns_lookup_hostname_options_callback
[`net.Server`]: #net_class_net_server
[`net.Socket`]: #net_class_net_socket
[`net.connect()`]: #net_net_connect
[`net.connect(options)`]: #net_net_connect_options_connectlistener
[`net.connect(path)`]: #net_net_connect_path_connectlistener
[`net.connect(port, host)`]: #net_net_connect_port_host_connectlistener
[`net.createConnection()`]: #net_net_createconnection
[`net.createConnection(options)`]: #net_net_createconnection_options_connectlistener
[`net.createConnection(path)`]: #net_net_createconnection_path_connectlistener
[`net.createConnection(port, host)`]: #net_net_createconnection_port_host_connectlistener
[`net.createServer()`]: #net_net_createserver_options_connectionlistener
[`new net.Socket(options)`]: #net_new_net_socket_options
[`server.close()`]: #net_server_close_callback
[`server.getConnections()`]: #net_server_getconnections_callback
[`server.listen()`]: #net_server_listen
[`server.listen(handle)`]: #net_server_listen_handle_backlog_callback
[`server.listen(options)`]: #net_server_listen_options_callback
[`server.listen(path)`]: #net_server_listen_path_backlog_callback
[`server.listen(port, host)`]: #net_server_listen_port_host_backlog_callback
[`socket.connect()`]: #net_socket_connect
[`socket.connect(options)`]: #net_socket_connect_options_connectlistener
[`socket.connect(path)`]: #net_socket_connect_path_connectlistener
[`socket.connect(port, host)`]: #net_socket_connect_port_host_connectlistener
[`socket.destroy()`]: #net_socket_destroy_exception
[`socket.end()`]: #net_socket_end_data_encoding
[`socket.pause()`]: #net_socket_pause
[`socket.resume()`]: #net_socket_resume
[`socket.setTimeout()`]: #net_socket_settimeout_timeout_callback
[`socket.setTimeout(timeout)`]: #net_socket_settimeout_timeout_callback
[`stream.setEncoding()`]: stream.html#stream_readable_setencoding_encoding
[IPC]: #net_ipc_support
[Identifying paths for IPC connections]: #net_identifying_paths_for_ipc_connections
[Readable Stream]: stream.html#stream_class_stream_readable
[duplex stream]: stream.html#stream_class_stream_duplex
[half-closed]: https://tools.ietf.org/html/rfc1122#section-4.2.2.13
[socket(7)]: http://man7.org/linux/man-pages/man7/socket.7.html
[unspecified IPv4 address]: https://en.wikipedia.org/wiki/0.0.0.0
[unspecified IPv6 address]: https://en.wikipedia.org/wiki/IPv6_address#Unspecified_address
