<!-- YAML
added: v0.1.30
changes:
  - version: v10.5.0
    pr-url: https://github.com/nodejs/node/pull/20220
    description: 接受额外的 `options` 对象，用于指定返回的数值是否为 bigint。
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `path` {string|Buffer|URL}
* `options` {Object}
  * `bigint` {boolean} 返回的 [`fs.Stats`] 对象中的数值是否应为 `bigint` 型。**默认值:** `false`。
* `callback` {Function}
  * `err` {Error}
  * `stats` {fs.Stats}

异步的 lstat(2)。
回调会传入两个参数 `(err, stats)`，其中 `stats` 是 [`fs.Stats`] 对象。
`lstat()` 与 [`stat()`] 相同，只是如果 `path` 是符号链接，则查看的是链接自身，而不是它指向的文件。

