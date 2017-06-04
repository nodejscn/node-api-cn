<!-- YAML
added: v0.1.29
changes:
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `data` parameter can now be a `Uint8Array`.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|integer} 文件名或文件描述符
* `data` {string|Buffer|Uint8Array}
* `options` {Object|string}
  * `encoding` {string|null} 默认 = `'utf8'`
  * `mode` {integer} 默认 = `0o666`
  * `flag` {string} 默认 = `'w'`
* `callback` {Function}

异步地写入数据到文件，如果文件已经存在，则替代文件。
`data` 可以是一个字符串或一个 buffer。

如果 `data` 是一个 buffer，则忽略 `encoding` 选项。它默认为 `'utf8'`。

例子：

```js
fs.writeFile('message.txt', 'Hello Node.js', (err) => {
  if (err) throw err;
  console.log('The file has been saved!');
});
```

如果 `options` 是一个字符串，则它指定了字符编码。例如：

```js
fs.writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
```

任何指定的文件描述符必须支持写入。

注意，多次对同一文件使用 `fs.writeFile` 且不等待回调，是不安全的。
对于这种情况，强烈推荐使用 `fs.createWriteStream`。

**注意：如果 `file` 指定为一个文件描述符，则它不会被自动关闭。**

