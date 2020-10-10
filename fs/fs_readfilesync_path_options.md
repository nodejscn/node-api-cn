<!-- YAML
added: v0.1.8
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `path` 可以是文件描述符。
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `null`。
  * `flag` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。
    **默认值:** `'r'`。
* 返回: {string|Buffer}

返回 `path` 的内容。

详见此 API 的异步版本的文档：[`fs.readFile()`]。

如果指定了 `encoding` 选项，则此函数返回字符串。
否则，返回 buffer。

与 [`fs.readFile()`] 相似，当路径是目录时，`fs.readFileSync()` 的行为是特定于平台的。

```js
// 在 macOS、Linux 和 Windows 上：
fs.readFileSync('<目录>');
// => [Error: EISDIR: illegal operation on a directory, read <目录>]

// 在 FreeBSD 上：
fs.readFileSync('<目录>'); // => <data>
```

