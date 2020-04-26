<!-- YAML
added: v0.6.7
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: 传入的 `options` 对象无法再被修改。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `file` 可以是文件描述符。
-->

* `path` {string|Buffer|URL|number} 文件名或文件描述符。
* `data` {string|Buffer}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。**默认值:** `'a'`。
* `callback` {Function}
  * `err` {Error}

异步地将数据追加到文件，如果文件尚不存在则创建该文件。
`data` 可以是字符串或 [`Buffer`]。

```js
fs.appendFile('message.txt', '追加的数据', (err) => {
  if (err) throw err;
  console.log('数据已追加到文件');
});
```

如果 `options` 是字符串，则它指定字符编码：

```js
fs.appendFile('message.txt', '追加的数据', 'utf8', callback);
```

`path` 可以指定为已打开用于追加（使用 `fs.open()` 或 `fs.openSync()`）的数字型文件描述符。
文件描述符不会自动关闭。

```js
fs.open('message.txt', 'a', (err, fd) => {
  if (err) throw err;
  fs.appendFile(fd, '追加的数据', 'utf8', (err) => {
    fs.close(fd, (err) => {
      if (err) throw err;
    });
    if (err) throw err;
  });
});
```


