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
* `encoding` {string} **默认值:** `'utf8'`。
* `callback` {Function}
  * `err` {Error}
  * `written` {integer}
  * `string` {string}

将 `string` 写入到 `fd` 指定的文件。
如果 `string` 不是一个字符串，则该值会被强制转换为字符串。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。
参阅 pwrite(2)。

`encoding` 是期望的字符串编码。

回调会接收到参数 `(err, written, string)`，其中 `written` 指定传入的字符串中被要求写入的字节数。
被写入的字节数不一定与被写入的字符串字符数相同。
参阅 [`Buffer.byteLength`]。

在同一个文件上多次使用 `fs.write()` 且不等待回调是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。
内核会忽略位置参数，并始终将数据追加到文件的末尾。

在 Windows 上，如果文件描述符连接到控制台（例如 `fd == 1` 或 `stdout`），则无论使用何种编码，包含非 ASCII 字符的字符串默认情况下都不会被正确地渲染。
通过使用 `chcp 65001` 命令更改活动的代码页，可以将控制台配置为正确地渲染 UTF-8。
详见 [chcp] 文档。

