<!-- YAML
added: v0.11.5
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: The `position` parameter is optional now.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
-->

* `fd` {integer}
* `string` {string}
* `position` {integer}
* `encoding` {string} 默认为 `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `written` {integer}
  * `string` {string}

将 `string` 写入到 `fd` 指定的文件。
如果 `string` 不是一个字符串，则会强制转换成字符串。

`position` 指定文件中要开始写入的偏移量。
如果 `typeof position !== 'number'`，则从当前位置开始写入。参见 pwrite(2)。

`encoding` 指定字符串的编码。

`callback` 有三个参数 `(err, written, string)`，其中 `written` 指定字符串中已写入文件的字节数。
写入的字节数与字符串的字符数是不同的。参见 [`Buffer.byteLength`]。

对同一文件多次使用 `fs.write()` 且不等待回调，是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，不能指定写入的位置。
内核会忽略位置参数，总是将数据追加到文件的尾部。

