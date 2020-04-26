<!-- YAML
added: v0.11.5
changes:
  - version: v14.0.0
    pr-url: https://github.com/nodejs/node/pull/31030
    description: The `string` parameter won't coerce unsupported input to
                 strings anymore.
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/7856
    description: The `position` parameter is optional now.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
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
如果 `string` 不是一个字符串，则会抛出异常。

`position` 指定文件开头的偏移量（数据应该被写入的位置）。
如果 `typeof position !== 'number'`，则数据会被写入当前的位置。
参见 pwrite(2)。

`encoding` 是期望的字符串编码。

回调会接收到参数 `(err, written, string)`，其中 `written` 指定传入的字符串中被要求写入的字节数。
被写入的字节数不一定与被写入的字符串字符数相同。
参见 [`Buffer.byteLength`]。

不等待回调就对同一个文件多次使用 `fs.write()` 是不安全的。
对于这种情况，建议使用 [`fs.createWriteStream()`]。

在 Linux 上，当以追加模式打开文件时，写入无法指定位置。
内核会忽略位置参数，并始终将数据追加到文件的末尾。

在 Windows 上，如果文件描述符连接到控制台（例如 `fd == 1` 或 `stdout`），则无论使用何种编码，包含非 ASCII 字符的字符串默认情况下都不会被正确地渲染。
通过使用 `chcp 65001` 命令更改活动的代码页，可以将控制台配置为正确地渲染 UTF-8。
详见 [chcp] 文档。

