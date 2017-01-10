
Use of `readable.push('')` is not recommended.

Pushing a zero-byte string or `Buffer` to a stream that is not in object mode
has an interesting side effect. Because it *is* a call to
[`readable.push()`][stream-push], the call will end the reading process.
However, because the argument is an empty string, no data is added to the
readable buffer so there is nothing for a user to consume.

[`'data'`]: #stream_event_data
[`'drain'`]: #stream_event_drain
[`'end'`]: #stream_event_end
[`'finish'`]: #stream_event_finish
[`'readable'`]: #stream_event_readable
[`EventEmitter`]: events.html#events_class_eventemitter
[`process.stderr`]: process.html#process_process_stderr
[`process.stdin`]: process.html#process_process_stdin
[`process.stdout`]: process.html#process_process_stdout
[`stream.cork()`]: #stream_writable_cork
[`stream.pipe()`]: #stream_readable_pipe_destination_options
[`stream.uncork()`]: #stream_writable_uncork
[`stream.unpipe()`]: #stream_readable_unpipe_destination
[`stream.wrap()`]: #stream_readable_wrap_stream
[API for Stream Consumers]: #stream_api_for_stream_consumers
[API for Stream Implementers]: #stream_api_for_stream_implementers
[child process stdin]: child_process.html#child_process_child_stdin
[child process stdout and stderr]: child_process.html#child_process_child_stdout
[Compatibility]: #stream_compatibility_with_older_node_js_versions
[crypto]: crypto.html
[Duplex]: #stream_class_stream_duplex
[fs read streams]: fs.html#fs_class_fs_readstream
[fs write streams]: fs.html#fs_class_fs_writestream
[`fs.createReadStream()`]: fs.html#fs_fs_createreadstream_path_options
[`fs.createWriteStream()`]: fs.html#fs_fs_createwritestream_path_options
[`net.Socket`]: net.html#net_class_net_socket
[`zlib.createDeflate()`]: zlib.html#zlib_zlib_createdeflate_options
[HTTP requests, on the client]: http.html#http_class_http_clientrequest
[HTTP responses, on the server]: http.html#http_class_http_serverresponse
[http-incoming-message]: http.html#http_class_http_incomingmessage
[Readable]: #stream_class_stream_readable
[stream-_flush]: #stream_transform_flush_callback
[stream-_read]: #stream_readable_read_size_1
[stream-_transform]: #stream_transform_transform_chunk_encoding_callback
[stream-_write]: #stream_writable_write_chunk_encoding_callback_1
[stream-_writev]: #stream_writable_writev_chunks_callback
[stream-end]: #stream_writable_end_chunk_encoding_callback
[stream-pause]: #stream_readable_pause
[stream-push]: #stream_readable_push_chunk_encoding
[stream-read]: #stream_readable_read_size
[stream-resume]: #stream_readable_resume
[stream-write]: #stream_writable_write_chunk_encoding_callback
[TCP sockets]: net.html#net_class_net_socket
[Transform]: #stream_class_stream_transform
[Writable]: #stream_class_stream_writable
[zlib]: zlib.html
[`Symbol.hasInstance`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol/hasInstance
