<!-- YAML
added: v0.0.2
changes:
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/18801
    description: The `as` and `as+` modes are supported now.
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using `file:`
                 protocol. Support is currently still *experimental*.
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} 请参阅[文件系统标志的支持][support of file system `flags`]。
* `mode` {integer} 默认为 `0o666`（可读写）。
* `callback` {Function}
  * `err` {Error}
  * `fd` {integer}

异步地打开文件。参阅 open(2)。

`mode` 设置文件模式（权限和粘滞位），但仅限于创建文件的情况。 
在 Windows 上，只能操作写权限。
参阅 [`fs.chmod()`]。

回调有两个参数 `(err, fd)`。

有些字符 (如 `< > : " / \ | ? *`) 在 Windows 上是保留的，参阅[命名文件、路径以及命名空间][Naming Files, Paths, and Namespaces]。 
在 NTFS 上，如果文件名包含冒号，则 Node.js 将打开文件系统流，参阅[此 MSDN 文档][MSDN-Using-Streams]。

基于 `fs.open()` 的函数也表现出以上行为，比如 `fs.writeFile()`、`fs.readFile()` 等。

