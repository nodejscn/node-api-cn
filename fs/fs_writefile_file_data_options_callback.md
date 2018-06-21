<!-- YAML
added: v0.1.29
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。
    		 不传入则运行时会抛出 `TypeError`。[CODE][CODE_fs.writeFile_6]
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `data` 现在可以是一个 `Uint8Array`。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
                 不传入会触发 id 为 DEP0013 的不建议使用警告。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `path` 现在可以是一个文件描述符。
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|Uint8Array}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`。
  * `mode` {integer} 默认为 `0o666`。
  * `flag` {string} 详见[支持的文件系统flag]。默认为 `'w'`。
* `callback` {Function}
  * `err` {Error}

异步地写入数据到文件，如果文件已经存在，则覆盖文件。
`data` 可以是字符串或 buffer。[CODE][CODE_fs.writeFile_1]

如果 `data` 是一个 buffer，则 `encoding` 选项无效。[CODE][CODE_fs.writeFile_2]

例子：

```js
fs.writeFile('message.txt', 'Hello Node.js', (err) => {
  if (err) throw err;
  console.log('The file has been saved!');
});
```

如果 `options` 是一个字符串，则它指定了字符编码。例子：[CODE][CODE_fs.writeFile_3]

```js
fs.writeFile('message.txt', 'Hello Node.js', 'utf8', callback);
```

任何指定的文件描述符必须支持写入。

对同一文件多次使用 `fs.writeFile` 且不等待回调，是不安全的。
对于这种情况，建议使用 `fs.createWriteStream`。

如果 `file` 是一个文件描述符，则它不会被自动关闭。

