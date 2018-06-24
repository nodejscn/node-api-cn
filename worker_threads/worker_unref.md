<!-- YAML
added: v10.5.0
-->

Calling `unref()` on a worker will allow the thread to exit if this is the only
active handle in the event system. If the worker is already `unref()`ed calling
`unref()` again will have no effect.

[`Buffer`]: buffer.html
[`EventEmitter`]: events.html
[`MessagePort`]: #worker_threads_class_messageport
[`port.postMessage()`]: #worker_threads_port_postmessage_value_transferlist
[`Worker`]: #worker_threads_class_worker
[`worker.terminate()`]: #worker_threads_worker_terminate_callback
[`worker.postMessage()`]: #worker_threads_worker_postmessage_value_transferlist_1
[`worker.on('message')`]: #worker_threads_event_message_1
[`worker.threadId`]: #worker_threads_worker_threadid_1
[`port.on('message')`]: #worker_threads_event_message
[`process.exit()`]: process.html#process_process_exit_code
[`process.abort()`]: process.html#process_process_abort
[`process.chdir()`]: process.html#process_process_chdir_directory
[`process.env`]: process.html#process_process_env
[`process.stdin`]: process.html#process_process_stdin
[`process.stderr`]: process.html#process_process_stderr
[`process.stdout`]: process.html#process_process_stdout
[`process.title`]: process.html#process_process_title
[`require('worker_threads').workerData`]: #worker_threads_worker_workerdata
[`require('worker_threads').on('workerMessage')`]: #worker_threads_event_workermessage
[`require('worker_threads').postMessage()`]: #worker_threads_worker_postmessage_value_transferlist
[`require('worker_threads').isMainThread`]: #worker_threads_worker_ismainthread
[`require('worker_threads').threadId`]: #worker_threads_worker_threadid
[`cluster` module]: cluster.html
[`inspector`]: inspector.html
[v8.serdes]: v8.html#v8_serialization_api
[`SharedArrayBuffer`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer
[Signals events]: process.html#process_signal_events
[`Uint8Array`]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array
[browser `MessagePort`]: https://developer.mozilla.org/en-US/docs/Web/API/MessagePort
[child processes]: child_process.html
[HTML structured clone algorithm]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm
[Web Workers]: https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API
