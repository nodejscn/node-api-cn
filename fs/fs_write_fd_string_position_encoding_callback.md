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

写入 `string` 到 `fd` 指定的文件。
如果 `string` 不是一个字符串，则该值将被强制转换为字符串。

`position` 指向从文件开始写入数据的位置的偏移量。
如果 `typeof position !== 'number'`，则数据从当前位置写入。参考 pwrite(2)。

`encoding` 是期望的字符串编码。

回调有三个参数 `(err, written, string)`，其中 `written` 指定传入的字符串被写入多少字节。
写入的字节与字符串的字符是不同的。参考 [`Buffer.byteLength`]。

多次对同一文件使用 `fs.write()` 且不等待回调，是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当文件以追加模式打开时，指定位置的写入是不起作用的。
内核会忽略位置参数，并总是将数据追加到文件的末尾。

