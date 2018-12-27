<!-- YAML
added: v0.1.29
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: The `data` parameter can now be any `TypedArray` or a
                 `DataView`.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: The `data` parameter can now be a `Uint8Array`.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: The `file` parameter can be a file descriptor now.
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|TypedArray|DataView}
* `options` {Object|string}
  * `encoding` {string|null} 默认为 `'utf8'`。
  * `mode` {integer} 默认为 `0o666`。
  * `flag` {string} 详见[支持的 flag][support of file system `flags`]。默认为 `'w'`。
* `callback` {Function}
  * `err` {Error}

异步地将数据写入文件，如果文件已存在，则覆盖文件。

如果 `data` 是一个 buffer，则忽略 `encoding`。

```js
const data = new Uint8Array(Buffer.from('Node.js中文网'));
fs.writeFile('文件.txt', data, (err) => {
  if (err) throw err;
  console.log('文件已保存');
});
```

如果 `options` 是一个字符串，则指定字符编码：

```js
fs.writeFile('文件.txt', 'Node.js中文网', 'utf8', callback);
```

对同一个文件多次使用 `fs.writeFile()` 且不等待回调，是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。


