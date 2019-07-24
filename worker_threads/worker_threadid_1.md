<!-- YAML
added: v10.5.0
-->

* {integer}

An integer identifier for the referenced thread. Inside the worker thread,
it is available as [`require('worker_threads').threadId`][].
This value is unique for each `Worker` instance inside a single process.

