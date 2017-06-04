<!-- YAML
added: v0.1.29
changes:
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `data` parameter can now be a `Uint8Array`.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|integer} 文件名或文件描述符
* `data` {string|Buffer|Uint8Array}
* `options` {Object|string}
  * `encoding` {string|null} 默认 = `'utf8'`
  * `mode` {integer} 默认 = `0o666`
  * `flag` {string} 默认 = `'w'`

[`fs.writeFile()`] 的同步版本。返回 `undefined`。

