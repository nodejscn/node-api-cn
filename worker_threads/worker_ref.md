<!-- YAML
added: v10.5.0
-->

Opposite of `unref()`, calling `ref()` on a previously `unref()`ed worker does
*not* let the program exit if it's the only active handle left (the default
behavior). If the worker is `ref()`ed, calling `ref()` again has
no effect.

