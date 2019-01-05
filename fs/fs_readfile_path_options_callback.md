<!-- YAML
added: v0.1.29
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v5.1.0
    pr-url: https://github.com/nodejs/node/pull/3740
    description: The `callback` will always be called with `null` as the `error`
                 parameter in case of success.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `path` parameter can be a file descriptor now.
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `null`。
  * `flag` {string} 请参阅[文件系统标志的支持][support of file system `flags`]。默认为 `'r'`。
* `callback` {Function}
  * `err` {Error}
  * `data` {string|Buffer}

异步地读取文件的内容。

```js
fs.readFile('/etc/passwd', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

`callback` 有两个参数 `(err, data)`，其中 `data` 是文件的内容。

如果没有指定 `encoding`，则返回原始的 buffer。

如果 `options` 是一个字符串，则指定字符编码：

```js
fs.readFile('/etc/passwd', 'utf8', callback);
```

如果 `path` 是一个目录，则 `fs.readFile()` 与 [`fs.readFileSync()`] 的行为因平台而异。
在 macOS、Linux 与 Windows 上，会返回错误。
在 FreeBSD 上，会返回目录内容的描述。

```js
// 在 macOS、Linux 与 Windows 上：
fs.readFile('<目录>', (err, data) => {
  // => [Error: EISDIR: illegal operation on a directory, read <directory>]
});

// 在 FreeBSD 上：
fs.readFile('<目录>', (err, data) => {
  // => null, <data>
});
```

`fs.readFile()` 会缓存整个文件。
为了最小化内存占用，尽可能优先使用 `fs.createReadStream()`。

