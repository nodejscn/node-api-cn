<!-- YAML
added: v15.4.0
-->

Calling `unref()` on a BroadcastChannel allows the thread to exit if this
is the only active handle in the event system. If the BroadcastChannel is
already `unref()`ed calling `unref()` again has no effect.

