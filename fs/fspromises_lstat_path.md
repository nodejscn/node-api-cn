<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* Returns: {Promise}

Asynchronous lstat(2). The `Promise` is resolved with the [`fs.Stats`][] object
for the given symbolic link `path`.

