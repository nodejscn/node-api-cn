<!-- YAML
added: v0.1.8
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是一个使用 `file:` 协议的 WHATWG `URL` 对象。该支持目前仍为试验性的。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `path` 现在可以是一个文件描述符。
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `null`。
  * `flag` {string} 详见[支持的文件系统标志][support of file system `flags`]。默认为 `'r'`。
* 返回: {string|Buffer}

返回文件 `path` 的内容。

详见异步版本的接口：[`fs.readFile()`]。

如果指定了 `encoding` 选项，则该函数返回一个字符串，否则返回一个 buffer。

与 [`fs.readFile()`] 相似, 当路径是一个目录时，`fs.readFileSync()` 的行为与平台有关。

```js
// 在 macOS、Linux 与 Windows 上：
fs.readFileSync('<目录>');
// => [Error: EISDIR: illegal operation on a directory, read <directory>]

// 在 FreeBSD 上：
fs.readFileSync('<目录>'); // => <data>
```

