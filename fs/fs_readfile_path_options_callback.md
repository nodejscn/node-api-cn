<!-- YAML
added: v0.1.29
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。不传入则运行时会抛出 `TypeError`。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是一个使用 `file:` 协议的 WHATWG `URL` 对象。该支持目前仍为试验性的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。不传入会触发 id 为 DEP0013 的不建议使用警告。
  - version: v5.1.0
    pr-url: https://github.com/nodejs/node/pull/3740
    description: 如果成功，则 `callback` 被调用时 `error` 参数总是为 `null`。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `path` 现在可以是一个文件描述符。
-->

* `path` {string|Buffer|URL|integer} 文件名或文件描述符。
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `null`。
  * `flag` {string} 详见[支持的文件系统flag]。默认为 `'r'`。
* `callback` {Function}
  * `err` {Error}
  * `data` {string|Buffer}

异步地读取一个文件的全部内容。
例子：

```js
fs.readFile('/etc/passwd', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

回调有两个参数 `(err, data)`，其中 `data` 是文件的内容。

如果未指定字符编码，则返回原始的 buffer。

如果 `options` 是一个字符串，则它指定了字符编码。
例子：

```js
fs.readFile('/etc/passwd', 'utf8', callback);
```

当 `path` 是一个目录时，`fs.readFile()` 与 [`fs.readFileSync()`] 的行为与平台有关。
在 macOS、Linux 与 Windows 上，会返回一个错误。
在 FreeBSD 上，会返回目录内容的描述。

```js
// 在 macOS、Linux 与 Windows 上：
fs.readFile('<directory>', (err, data) => {
  // => [Error: EISDIR: illegal operation on a directory, read <directory>]
});

// 在 FreeBSD 上：
fs.readFile('<directory>', (err, data) => {
  // => null, <data>
});
```

任何指定的文件描述符必须支持读取。

如果 `path` 是一个文件描述符，则它不会被自动关闭。

`fs.readFile()` 函数会缓存整个文件。
为了最小化内存占用，尽可能优先使用 `fs.createReadStream()`。

