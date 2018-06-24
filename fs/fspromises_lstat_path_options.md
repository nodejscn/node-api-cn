<!-- YAML
added: v10.0.0
changes:
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: Accepts an additional `options` object to specify whether
                 the numeric values returned should be bigint.
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `bigint` {boolean} Whether the numeric values in the returned
    [`fs.Stats`][] object should be `bigint`. **Default:** `false`.
* Returns: {Promise}

Asynchronous lstat(2). The `Promise` is resolved with the [`fs.Stats`][] object
for the given symbolic link `path`.

