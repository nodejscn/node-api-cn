<!-- YAML
added: v0.6.7
-->

* `file` {String | Buffer | Number} 文件名或文件描述符
* `data` {String | Buffer}
* `options` {Object | String}
  * `encoding` {String | Null} 默认 = `'utf8'`
  * `mode` {Integer} 默认 = `0o666`
  * `flag` {String} 默认 = `'a'`
* `callback` {Function}

异步地追加数据到一个文件，如果文件不存在则创建文件。
`data` 可以是一个字符串或 buffer。

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

任何指定的文件描述符必须为了追加而被打开。

注意：如果文件描述符被指定为 `file`，则不会被自动关闭。

