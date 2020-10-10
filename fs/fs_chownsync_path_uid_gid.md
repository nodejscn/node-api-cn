<!-- YAML
added: v0.1.97
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `uid` {integer}
* `gid` {integer}

同步地更改文件的所有者和群组。
返回 `undefined`。
这是 [`fs.chown()`] 的同步版本。

也可参见 chown(2)。

