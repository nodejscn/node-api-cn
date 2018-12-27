<!-- YAML
added: v0.6.7
changes:
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
  * `flag` {string} 详见[支持的 flag][support of file system `flags`]。默认为 `'a'`。

同步地将数据追加到文件，如果文件不存在则创建文件。

```js
try {
  fs.appendFileSync('文件.txt', '追加的数据');
  console.log('数据已追加到文件');
} catch (err) {
  /* 异常处理 */
}
```

如果 `options` 是一个字符串，则指定字符编码：

```js
fs.appendFileSync('文件.txt', '追加的数据', 'utf8');
```

`path` 可以是使用 `fs.open()` 或者 `fs.openSync()` 打开的文件描述符。
文件描述符不会自动关闭。

```js
let fd;

try {
  fd = fs.openSync('文件.txt', 'a');
  fs.appendFileSync(fd, '追加的数据', 'utf8');
} catch (err) {
  /* 异常处理 */
} finally {
  if (fd !== undefined)
    fs.closeSync(fd);
}
```


