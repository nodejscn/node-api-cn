<!-- YAML
added: v0.1.31
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/13028
    description: Pipe/Socket resolve support was added.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
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
  * `encoding` {string} 默认为 `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `resolvedPath` {string|Buffer}

异步地计算文件路径，解析 `.`、`..` 与符号链接。

该函数与 realpath(3) 的区别在于：

1. 在大小写不敏感的文件系统，不会执行大小写转换。

2. 符号链接的最大数量与平台无关，通常大于原生 realpath(3) 的。

`callback` 有两个参数 `(err, resolvedPath)`。
可以使用 `process.cwd` 解析相对路径。

只支持可转换成 UTF8 字符串的路径。

可选的 `options` 参数用于传入回调的路径，它可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。
如果 `encoding` 设为 `'buffer'`，则返回的路径会被作为 `Buffer` 对象传入。

如果 `path` 解析到 socket 或管道，则函数会返回与该对象相关的系统名称。


