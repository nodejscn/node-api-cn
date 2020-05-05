<!-- YAML
added: v0.1.21
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `oldPath` 和 `newPath` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `oldPath` {string|Buffer|URL}
* `newPath` {string|Buffer|URL}

同步的 rename(2)。返回 `undefined`。

