<!-- YAML
added: v0.7.0
-->

* {Object}

A hash that stores the active worker objects, keyed by `id` field. Makes it
easy to loop through all the workers. It is only available in the master
process.

A worker is removed from cluster.workers after the worker has disconnected _and_
exited. The order between these two events cannot be determined in advance.
However, it is guaranteed that the removal from the cluster.workers list happens
before last `'disconnect'` or `'exit'` event is emitted.

```js
// Go through all workers
function eachWorker(callback) {
  for (var id in cluster.workers) {
    callback(cluster.workers[id]);
  }
}
eachWorker((worker) => {
  worker.send('big announcement to all workers');
});
```

Should you wish to reference a worker over a communication channel, using
the worker's unique id is the easiest way to find the worker.

```js
socket.on('data', (id) => {
  var worker = cluster.workers[id];
});
```

[`child_process.fork()`]: child_process.html#child_process_child_process_fork_modulepath_args_options
[`ChildProcess.send()`]: child_process.html#child_process_child_send_message_sendhandle_options_callback
[`disconnect`]: child_process.html#child_process_child_disconnect
[`kill`]: process.html#process_process_kill_pid_signal
[`server.close()`]: net.html#net_event_close
[`worker.exitedAfterDisconnect`]: #cluster_worker_exitedafterdisconnect
[Child Process module]: child_process.html#child_process_child_process_fork_modulepath_args_options
[child_process event: 'exit']: child_process.html#child_process_event_exit
[child_process event: 'message']: child_process.html#child_process_event_message
[`process` event: `'message'`]: process.html#process_event_message
