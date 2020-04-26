<!-- YAML
added: v0.1.31
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/13028
    description: Pipe/Socket resolve support was added.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
  - version: v6.4.0
    pr-url: https://github.com/nodejs/node/pull/7899
    description: Calling `realpath` now works again for various edge cases
                 on Windows.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/3594
    description: The `cache` parameter was removed.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `resolvedPath` {string|Buffer}

通过解析 `.`、`..` 和符号链接异步地计算规范路径名。

规范路径名不一定是唯一的。
硬链接和绑定装载可以通过许多路径名暴露文件系统实体。

此函数的行为类似于 realpath(3)，但有一些例外：

1. 在不区分大小写的文件系统上不执行大小写转换。。

2. 符号链接的最大数量与平台无关，并且通常高于本地 realpath(3) 实现支持的数量。

`callback` 有两个参数 `(err, resolvedPath)`。
可以使用 `process.cwd` 来解析相对路径。

仅支持可转换为 UTF8 字符串的路径。

可选的 `options` 参数可以是指定编码的字符串，也可以是具有 `encoding` 属性的对象，该属性指定用于传递给回调的路径的字符编码。
如果 `encoding` 设置为 `'buffer'`，则返回的路径将作为 `Buffer` 对象传入。

如果 `path` 解析为套接字或管道，则该函数将返回该对象的系统相关名称。


