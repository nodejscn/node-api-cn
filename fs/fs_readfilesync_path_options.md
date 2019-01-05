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
  * `encoding` {string|null} 默认为 `null`。
  * `flag` {string} 请参阅[文件系统标志的支持][support of file system `flags`]。默认为 `'r'`。
* 返回: {string|Buffer}

返回文件的内容。

详见异步的方法 [`fs.readFile()`]。

如果指定了 `encoding`，则返回字符串，否则返回 buffer。

如果 `path` 是一个目录，则 `fs.readFileSync()` 的行为因平台而异。

```js
// 在 macOS、Linux 与 Windows 上：
fs.readFileSync('<目录>');
// => [Error: EISDIR: illegal operation on a directory, read <directory>]

// 在 FreeBSD 上：
fs.readFileSync('<目录>'); // => <data>
```

