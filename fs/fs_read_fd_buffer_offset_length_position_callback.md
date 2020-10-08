<!-- YAML
added: v0.0.2
changes:
  - version: v10.10.0
    pr-url: https://github.com/nodejs/node/pull/22150
    description: 参数 `buffer` 可以是任何 `TypedArray` 或 `DataView`。
  - version: v7.4.0
    pr-url: https://github.com/nodejs/node/pull/10382
    description: 参数 `buffer` 可以是 `Uint8Array`。
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4518
    description: 参数 `length` 可以为 `0`。
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* `callback` {Function}
  * `err` {Error}
  * `bytesRead` {integer}
  * `buffer` {Buffer}

从 `fd` 指定的文件中读取数据。

`buffer` 是数据（从 fd 读取）要被写入的 buffer。

`offset` 是 buffer 中开始写入的偏移量。

`length` 是整数，指定要读取的字节数。

`position` 参数指定从文件中开始读取的位置。
如果 `position` 为 `null`，则从当前文件位置读取数据，并更新文件位置。
如果 `position` 是整数，则文件位置会保持不变。

回调有三个参数 `(err, bytesRead, buffer)`。

如果文件没有被同时地修改，则当读取的字节数为零时，即到达文件的末尾。

如果调用此方法的 [`util.promisify()`] 版本，则返回 `Promise`（会传入具有 `bytesRead` 属性和 `buffer` 属性的 `Object`）。

