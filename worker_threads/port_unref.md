<!-- YAML
added: v10.5.0
-->

Calling `unref()` on a port will allow the thread to exit if this is the only
active handle in the event system. If the port is already `unref()`ed calling
`unref()` again will have no effect.

If listeners are attached or removed using `.on('message')`, the port will
be `ref()`ed and `unref()`ed automatically depending on whether
listeners for the event exist.

