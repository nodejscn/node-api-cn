<!-- YAML
added: v0.1.8
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `path` parameter can be a file descriptor now.
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `null`。
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'r'`。
* 返回: {string|Buffer}

返回 `path` 的内容。

有关详细信息，参阅此 API 的异步版本的文档：[`fs.readFile()`]。

如果指定了 `encoding` 选项，则此函数返回字符串，否则返回 buffer。

与 [`fs.readFile()`] 类似，当 `path` 是目录时，`fs.readFileSync()` 的行为是特定于平台的。

```js
// 在 macOS、Linux 和 Windows 上：
fs.readFileSync('<目录>');
// => [Error: EISDIR: illegal operation on a directory, read <目录>]

// 在 FreeBSD 上：
fs.readFileSync('<目录>'); // => <data>
```

