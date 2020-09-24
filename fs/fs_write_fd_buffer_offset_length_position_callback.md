<!-- YAML
added: v0.0.2
changes:
  - version: v14.12.0
    pr-url: https://github.com/nodejs/node/pull/34993
    description: 参数 `buffer` 会使用显式的 `toString` 函数对对象进行字符串化。
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: 参数 `buffer` 不再强制把不支持的输入转换为字符串。
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: 参数 `buffer` 可以是任何 `TypedArray` 或 `DataView`。
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `buffer` 可以是 `Uint8Array`。
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: 参数 `offset` 和 `length` 是可选的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesWritten` {integer}
  * `buffer` {Buffer|TypedArray|DataView}

写入 `buffer` 到 `fd` 指定的文件。

`offset` 决定 buffer 中要被写入的部位，`length` 是整数，指定要写入的字节数。

`position` 指定文件开头的偏移量（数据要被写入的位置）。
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。
参见 pwrite(2)。

回调有三个参数 `(err, bytesWritten, buffer)`，其中 `bytesWritten` 指定从 `buffer` 中被写入的字节数。

如果调用此方法的 [`util.promisify()`] 版本，则返回 `Promise`（会传入具有 `bytesWritten` 和 `buffer` 属性的 `Object`）。

不等待回调就对同一个文件多次使用 `fs.write()` 是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，则写入时无法指定位置。
内核会忽略位置参数，并始终追加数据到文件的末尾。


