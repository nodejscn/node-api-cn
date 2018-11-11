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
* `flags` {string|number} 详见[支持的文件系统标志][support of file system `flags`]。
* `mode` {integer} 默认为 `0o666`。
* `callback` {Function}
  * `err` {Error}
  * `fd` {integer}

异步地打开文件。详见 open(2)。

`mode` 可设置文件的模式（权限和粘滞位），但只有创建文件时才有效。
在 Windows 上，只能操作写入权限。
参考 [`fs.chmod()`]。

该回调有两个参数 `(err, fd)`。

有些字符 (如 `< > : " / \ | ? *`) 在 Windows 下是被保留的，参考文档[命名文件、路径、命名空间][Naming Files, Paths, and Namespaces]。 
在 NTFS 下，如果文件名包含冒号，则 Node.js 会打开一个文件系统流，参考 [MSDN文档][MSDN-Using-Streams]。

基于 `fs.open()` 的函数也有以上特性，比如 `fs.writeFile()`、`fs.readFile()` 等。

