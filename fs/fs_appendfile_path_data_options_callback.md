<!-- YAML
added: v0.6.7
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `path` {string|Buffer|URL|number} 文件名或文件描述符。
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`。
  * `mode` {integer} 默认为 `0o666`。
  * `flag` {string} 详见[支持的文件系统标志][support of file system `flags`]。默认为 `'a'`。
* `callback` {Function}
  * `err` {Error}

异步地追加数据到文件，如果文件不存在则创建文件。
`data` 可以是字符串或 [`Buffer`]。

例子：

```js
fs.appendFile('文件.txt', '追加的数据', (err) => {
  if (err) throw err;
  console.log('数据已追加到文件');
});
```

如果 `options` 为字符串，则它指定了字符编码。例如：

```js
fs.appendFile('文件.txt', '追加的数据', 'utf8', callback);
```

`path` 也可以是使用 `fs.open()` 或者 `fs.openSync()` 打开的文件描述符。
文件描述符不会被自动关闭。

```js
fs.open('文件.txt', 'a', (err, fd) => {
  if (err) throw err;
  fs.appendFile(fd, '追加的数据', 'utf8', (err) => {
    fs.close(fd, (err) => {
      if (err) throw err;
    });
    if (err) throw err;
  });
});
```


