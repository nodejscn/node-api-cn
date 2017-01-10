<!-- YAML
added: v0.7.2
-->

* {Boolean} Set to `false` after `child.disconnect()` is called

The `child.connected` property indicates whether it is still possible to send
and receive messages from a child process. When `child.connected` is `false`, it
is no longer possible to send or receive messages.

