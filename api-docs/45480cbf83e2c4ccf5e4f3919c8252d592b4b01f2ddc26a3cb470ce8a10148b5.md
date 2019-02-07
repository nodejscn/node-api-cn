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
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'a'`。

同步地将数据追加到文件，如果文件尚不存在则创建该文件。
`data` 可以是字符串或 [`Buffer`]。

```js
try {
  fs.appendFileSync('message.txt', '追加的数据');
  console.log('数据已追加到文件');
} catch (err) {
  /* 处理错误 */
}
```

如果 `options` 是字符串，则它指定字符编码：

```js
fs.appendFileSync('message.txt', '追加的数据', 'utf8');
```

`path` 可以指定为已打开用于追加（使用 `fs.open()` 或 `fs.openSync()`）的数字型文件描述符。
文件描述符不会自动关闭。

```js
let fd;

try {
  fd = fs.openSync('message.txt', 'a');
  fs.appendFileSync(fd, '追加的数据', 'utf8');
} catch (err) {
  /* 处理错误 */
} finally {
  if (fd !== undefined)
    fs.closeSync(fd);
}
```


