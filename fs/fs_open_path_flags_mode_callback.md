<!-- YAML
added: v0.0.2
changes:
  - version: v11.1.0
    pr-url: https://github.com/nodejs/node/pull/23767
    description: 参数 `flags` 是可选的，并且默认为 `'r'`。
  - version: v9.9.0
    pr-url: https://github.com/nodejs/node/pull/18801
    description: 支持 `as` 和 `as+` 标志。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} 参见[文件系统 `flag` 的支持][support of file system `flags`]。
  **默认值:** `'r'`。
* `mode` {string|integer} **默认值:** `0o666`（可读写）。
* `callback` {Function}
  * `err` {Error}
  * `fd` {integer}

异步地打开文件。
参见 open(2)。

`mode` 用于设置文件模式（权限和粘滞位），但仅限于创建文件时。
在 Windows 上，只能操作写权限，参见 [`fs.chmod()`]。

回调有两个参数 `(err, fd)`。

有些字符 (`< > : " / \ | ? *`) 在 Windows 上是预留的，参见[命名文件、路径以及命名空间][Naming Files, Paths, and Namespaces]。 
在 NTFS 上，如果文件名包含冒号，则 Node.js 会打开文件系统流，参见[此 MSDN 页面][MSDN-Using-Streams]。

基于 `fs.open()` 的函数也会表现出以上行为，比如 `fs.writeFile()`、`fs.readFile()` 等。

