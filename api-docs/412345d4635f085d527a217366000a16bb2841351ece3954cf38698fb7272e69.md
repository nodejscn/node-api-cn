<!-- YAML
added: v0.1.21
changes:
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/21875
    description: The second argument can now be an `options` object with
                 `recursive` and `mode` properties.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {integer} Windows 上不支持。**默认值:** `0o777`。

同步地创建目录。
返回 `undefined`。
[`fs.mkdir()`] 的同步版本。

也可参阅 mkdir(2)。

