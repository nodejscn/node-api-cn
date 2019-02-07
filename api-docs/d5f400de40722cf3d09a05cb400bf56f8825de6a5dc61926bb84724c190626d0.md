<!-- YAML
added: v0.1.97
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `uid` {integer}
* `gid` {integer}

同步地更改文件的所有者和群组。
返回 `undefined`。
这是 [`fs.chown()`] 的同步版本。

也可参阅 chown(2)。

