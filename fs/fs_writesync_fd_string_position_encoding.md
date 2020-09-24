<!-- YAML
added: v0.11.5
changes:
  - version: v14.12.0
    pr-url: https://github.com/nodejs/node/pull/34993
    description: The `string` parameter will stringify an object with an
                 explicit `toString` function.
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: The `string` parameter won't coerce unsupported input to
                 strings anymore.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: The `position` parameter is optional now.
-->

* `fd` {integer}
* `string` {string|Object}
* `position` {integer}
* `encoding` {string}
* 返回: {number} 写入的字节数。

详见此 API 的异步版本的文档： [`fs.write(fd, string...)`]。

