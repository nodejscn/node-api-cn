
It is important to keep in mind that the `maxBuffer` option specifies the
largest number of *octets* allowed on `stdout` or `stderr`. If this value is
exceeded, then the child process is terminated. This particularly impacts
output that includes multibyte character encodings such as UTF-8 or UTF-16.
For instance, the following will output 13 UTF-8 encoded octets to `stdout`
although there are only 4 characters:

```js
console.log('中文测试');
```

[`'error'`]: #child_process_event_error
[`'exit'`]: #child_process_event_exit
[`'message'`]: #child_process_event_message
[`child.connected`]: #child_process_child_connected
[`child.disconnect()`]: #child_process_child_disconnect
[`child.kill()`]: #child_process_child_kill_signal
[`child.send()`]: #child_process_child_send_message_sendhandle_options_callback
[`child.stderr`]: #child_process_child_stderr
[`child.stdin`]: #child_process_child_stdin
[`child.stdout`]: #child_process_child_stdout
[`child_process.exec()`]: #child_process_child_process_exec_command_options_callback
[`child_process.execFile()`]: #child_process_child_process_execfile_file_args_options_callback
[`child_process.execFileSync()`]: #child_process_child_process_execfilesync_file_args_options
[`child_process.execSync()`]: #child_process_child_process_execsync_command_options
[`child_process.fork()`]: #child_process_child_process_fork_modulepath_args_options
[`child_process.spawn()`]: #child_process_child_process_spawn_command_args_options
[`child_process.spawnSync()`]: #child_process_child_process_spawnsync_command_args_options
[`ChildProcess`]: #child_process_child_process
[`Error`]: errors.html#errors_class_error
[`EventEmitter`]: events.html#events_class_eventemitter
[`JSON.stringify()`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[`maxBuffer`]: #child_process_maxbuffer_and_unicode
[`net.Server`]: net.html#net_class_net_server
[`net.Socket`]: net.html#net_class_net_socket
[`options.detached`]: #child_process_options_detached
[`process.disconnect()`]: process.html#process_process_disconnect
[`process.env`]: process.html#process_process_env
[`process.execPath`]: process.html#process_process_execpath
[`process.on('disconnect')`]: process.html#process_event_disconnect
[`process.on('message')`]: process.html#process_event_message
[`process.send()`]: process.html#process_process_send_message_sendhandle_options_callback
[`stdio`]: #child_process_options_stdio
[synchronous counterparts]: #child_process_synchronous_process_creation
