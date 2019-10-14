<!-- YAML
added: v12.12.0
-->

* Returns: {Promise}

Asynchronously close the directory's underlying resource handle.
Subsequent reads will result in errors.

A `Promise` is returned that will be resolved after the resource has been
closed.

