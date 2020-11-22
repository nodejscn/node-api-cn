<!-- YAML
added: v0.1.29
changes:
  - version: v14.12.0
    pr-url: https://github.com/nodejs/node/pull/34993
    description: 参数 `data` 会使用显式的 `toString` 函数对对象进行字符串化。
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: 参数 `data` 不再强制转换不支持的输入为字符串。
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: 参数 `data` 可以是任何的 `TypedArray` 或 `DataView`。
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `data` 可以是 `Uint8Array`。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
  - version: v5.0.0
    pr-url: https://github.com/nodejs/node/pull/3163
    description: 参数 `file` 可以是文件描述符。
-->

* `file` {string|Buffer|URL|integer} 文件名或文件描述符。
* `data` {string|Buffer|TypedArray|DataView}
* `options` {Object|string}
  * `encoding` {string|null} **默认值:** `'utf8'`。
  * `mode` {integer} **默认值:** `0o666`。
  * `flag` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。
    **默认值:** `'w'`。
* `callback` {Function}
  * `err` {Error}

当 `file` 是文件名时，则异步地写入数据到文件（如果文件已存在，则覆盖文件）。
`data` 可以是字符串或 buffer。

当 `file` 是文件描述符时，则其行为类似于直接调用 `fs.write()`（建议使用）。 
参见以下关于使用文件描述符的说明。

如果 `data` 是 buffer，则 `encoding` 选项会被忽略。
如果 `data` 是普通的对象，则它必须具有自身的 `toString` 函数属性。

```js
const data = new Uint8Array(Buffer.from('Node.js 中文网'));
fs.writeFile('文件.txt', data, (err) => {
  if (err) throw err;
  console.log('文件已被保存');
});
```

如果 `options` 是字符串，则它指定字符编码：

```js
fs.writeFile('文件.txt', 'Node.js 中文网', 'utf8', callback);
```

不等待回调就对同一个文件多次使用 `fs.writeFile()` 是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。


