<!-- YAML
added: v0.1.21
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4518
    description: The `length` parameter can now be `0`.
-->

* `fd` {integer}
* `buffer` {string|Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}

[`fs.read()`] 的同步版本。
返回 `bytesRead` 的数量。

