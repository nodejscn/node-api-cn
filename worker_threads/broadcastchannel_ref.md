<!-- YAML
added: v15.4.0
-->

Opposite of `unref()`. Calling `ref()` on a previously `unref()`ed
BroadcastChannel does *not* let the program exit if it's the only active handle
left (the default behavior). If the port is `ref()`ed, calling `ref()` again
has no effect.

