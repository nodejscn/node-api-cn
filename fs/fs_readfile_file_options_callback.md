<!-- YAML
added: v0.1.29
-->

* `file` {String | Buffer | Integer} 文件名或文件描述符
* `options` {Object | String}
  * `encoding` {String | Null} 默认 = `null`
  * `flag` {String} 默认 = `'r'`
* `callback` {Function}

异步的读取一个文件的全部内容。
例子：

```js
fs.readFile('/etc/passwd', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

回调有两个参数 `(err, data)`，其中 `data` 是文件的内容。

如果字符编码未指定，则返回原始的 buffer。

如果 `options` 是一个字符串，则它指定了字符编码。
例子：

```js
fs.readFile('/etc/passwd', 'utf8', callback);
```

任何指定的文件描述符必须支持读取。

注意，如果一个文件描述符被指定为 `file`，则它不会被自动关闭。

