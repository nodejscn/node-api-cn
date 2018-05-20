<!-- YAML
added: v0.6.7
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|URL|number} 文件名或文件描述符
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`
  * `mode` {integer} 默认为 `0o666`
  * `flag` {string} 默认为 `'a'`
* `callback` {Function}
  * `err` {Error}

异步地追加数据到一个文件，如果文件不存在则创建文件。
`data` 可以是一个字符串或 [`Buffer`]。

例子：

```js
fs.appendFile('message.txt', 'data to append', (err) => {
  if (err) throw err;
  console.log('The "data to append" was appended to file!');
});
```

如果 `options` 是一个字符串，则它指定了字符编码。例如：

```js
fs.appendFile('message.txt', 'data to append', 'utf8', callback);
```

`file` 可能是一个被打开用来追加数据的数字文件描述符（通过 `fs.open()` 或者 `fs.openSync()`）。这样的文件描述符将不会被自动关闭。

```js
fs.open('message.txt', 'a', (err, fd) => {
  if (err) throw err;
  fs.appendFile(fd, 'data to append', 'utf8', (err) => {
    fs.close(fd, (err) => {
      if (err) throw err;
    });
    if (err) throw err;
  });
});
```


