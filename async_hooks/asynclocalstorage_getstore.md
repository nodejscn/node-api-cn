<!-- YAML
added:
 - v13.10.0
 - v12.17.0
-->

* Returns: {any}

Returns the current store.
If called outside of an asynchronous context initialized by
calling `asyncLocalStorage.run()` or `asyncLocalStorage.enterWith()`, it
returns `undefined`.

