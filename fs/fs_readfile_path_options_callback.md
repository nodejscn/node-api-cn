<!-- YAML
added: v0.1.29
changes:
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
  - version: v5.1.0
    pr-url: https://github.com/nodejs/node/pull/3740
    description: 如果成功，则 `callback` 被调用时，`error` 参数始终为 `null`。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `path` 可以是文件描述符。
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `null`。
  * `flag` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。**默认值:** `'r'`。
* `callback` {Function}
  * `err` {Error}
  * `data` {string|Buffer}

异步地读取文件的全部内容。

```js
fs.readFile('文件名', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

回调会传入两个参数 `(err, data)`，其中 `data` 是文件的内容。

如果没有指定字符编码，则返回原始的 buffer。

如果 `options` 是字符串，则它指定字符编码：

```js
fs.readFile('文件名', 'utf8', callback);
```

当路径是目录时，则 `fs.readFile()` 和 [`fs.readFileSync()`] 的行为是特定于平台的。
在 macOS、Linux 和 Windows 上，会返回错误。
在 FreeBSD 上，会返回目录内容的表示。

```js
// 在 macOS、Linux 和 Windows 上：
fs.readFile('<目录>', (err, data) => {
  // => [Error: EISDIR: illegal operation on a directory, read <目录>]
});

// 在 FreeBSD 上：
fs.readFile('<目录>', (err, data) => {
  // => null, <data>
});
```

`fs.readFile()` 函数会缓冲整个文件。
若要最小化内存成本，则尽可能选择流式（使用 `fs.createReadStream()`）。

