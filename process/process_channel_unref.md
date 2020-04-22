<!-- YAML
added: v7.1.0
-->

This method makes the IPC channel not keep the event loop of the process
running, and lets it finish even while the channel is open.

Typically, this is managed through the number of `'disconnect'` and `'message'`
listeners on the `process` object. However, this method can be used to
explicitly request a specific behavior.

