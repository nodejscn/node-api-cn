<!-- YAML
added: v0.0.2
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `flags` {string|number}
* `mode` {integer} **Default:** `0o666`
* `callback` {Function}

异步地打开文件。详见 open(2)。
`flags` 可以是：

* `'r'` - 以读取模式打开文件。如果文件不存在则发生异常。

* `'r+'` - 以读写模式打开文件。如果文件不存在则发生异常。

* `'rs+'` - 以同步读写模式打开文件。命令操作系统绕过本地文件系统缓存。

  这对 NFS 挂载模式下打开文件很有用，因为它可以让你跳过潜在的旧本地缓存。
  它对 I/O 的性能有明显的影响，所以除非需要，否则不要使用此标志。

  注意，这不会使 `fs.open()` 进入同步阻塞调用。
  如果那是你想要的，则应该使用 `fs.openSync()`。

* `'w'` - 以写入模式打开文件。文件会被创建（如果文件不存在）或截断（如果文件存在）。

* `'wx'` - 类似 `'w'`，但如果 `path` 存在，则失败。

* `'w+'` - 以读写模式打开文件。文件会被创建（如果文件不存在）或截断（如果文件存在）。

* `'wx+'` - 类似 `'w+'`，但如果 `path` 存在，则失败。

* `'a'` - 以追加模式打开文件。如果文件不存在，则会被创建。

* `'ax'` - 类似于 `'a'`，但如果 `path` 存在，则失败。

* `'a+'` - 以读取和追加模式打开文件。如果文件不存在，则会被创建。

* `'ax+'` - 类似于 `'a+'`，但如果 `path` 存在，则失败。

`mode` 可设置文件模式（权限和 sticky 位），但只有当文件被创建时才有效。默认为 `0o666`，可读写。

该回调有两个参数 `(err, fd)`。

特有的标志 `'x'`（在 open(2) 中的 `O_EXCL` 标志）确保 `path` 是新创建的。
在 POSIX 操作系统中，`path` 会被视为存在，即使是一个链接到一个不存在的文件的符号。
该特有的标志有可能在网络文件系统中无法使用。

`flags` 也可以是一个数字，[open(2)] 文档中有描述；
常用的常量可从 `fs.constants` 获取。
在 Windows 系统中，标志会被转换为与它等同的替代者，例如，`O_WRONLY` 转换为 `FILE_GENERIC_WRITE`、或 `O_EXCL|O_CREAT` 转换为 `CREATE_NEW`，通过 CreateFileW 接受。

在 Linux 中，当文件以追加模式打开时，定位的写入不起作用。
内核会忽略位置参数，并总是附加数据到文件的末尾。

注意：`fs.open()` 某些标志的行为是与平台相关的。
因此，在 macOS 和 Linux 下用 `'a+'` 标志打开一个目录（见下面的例子），会返回一个错误。
与此相反，在 Windows 和 FreeBSD，则会返回一个文件描述符。

```js
// macOS 与 Linux
fs.open('<directory>', 'a+', (err, fd) => {
  // => [Error: EISDIR: illegal operation on a directory, open <directory>]
});

// Windows 与 FreeBSD
fs.open('<directory>', 'a+', (err, fd) => {
  // => null, <fd>
});
```

Some characters (`< > : " / \ | ? *`) are reserved under Windows as documented
by [Naming Files, Paths, and Namespaces][]. Under NTFS, if the filename contains
a colon, Node.js will open a file system stream, as described by
[this MSDN page][MSDN-Using-Streams].

Functions based on `fs.open()` exhibit this behavior as well. eg.
`fs.writeFile()`, `fs.readFile()`, etc.

