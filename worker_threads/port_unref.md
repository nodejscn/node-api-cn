<!-- YAML
added: v10.5.0
-->

Calling `unref()` on a port allows the thread to exit if this is the only
active handle in the event system. If the port is already `unref()`ed calling
`unref()` again has no effect.

If listeners are attached or removed using `.on('message')`, the port is
`ref()`ed and `unref()`ed automatically depending on whether
listeners for the event exist.

