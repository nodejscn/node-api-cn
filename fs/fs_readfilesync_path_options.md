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

* `path` {string|Buffer|URL|integer} 文件名或文件描述符
* `options` {Object|string}
  * `encoding` {string|null} 默认 = `null`
  * `flag` {string} 默认 = `'r'`

[`fs.readFile()`] 的同步版本。
返回 `path` 的内容。

如果指定了 `encoding` 选项，则该函数返回一个字符串，否则返回一个 buffer。

*Note*: Similar to [`fs.readFile()`][], when the path is a directory, the
behavior of `fs.readFileSync()` is platform-specific.

```js
// macOS, Linux and Windows
fs.readFileSync('<directory>');
// => [Error: EISDIR: illegal operation on a directory, read <directory>]

//  FreeBSD
fs.readFileSync('<directory>'); // => null, <data>
```

