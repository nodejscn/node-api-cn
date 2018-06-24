<!-- YAML
added: v10.5.0
-->

* {null|MessagePort}

If this thread was spawned as a [`Worker`][], this will be a [`MessagePort`][]
allowing communication with the parent thread. Messages sent using
`parentPort.postMessage()` will be available in the parent thread
using `worker.on('message')`, and messages sent from the parent thread
using `worker.postMessage()` will be available in this thread using
`parentPort.on('message')`.

