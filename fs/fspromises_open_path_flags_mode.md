<!-- YAML
added: v10.0.0
changes:
  - version: v11.1.0
    pr-url: https://github.com/nodejs/node/pull/23767
    description: 参数 `flags` 是可选的，并且默认为 `'r'`。
-->

* `path` {string|Buffer|URL}
* `flags` {string|number} 参见[文件系统 `flag` 的支持][support of file system `flags`]。**默认值:** `'r'`。
* `mode` {string|integer} **默认值:** `0o666`（可读写）。
* 返回: {Promise}

异步地打开文件并返回一个 `Promise`，当解决时会带上一个 `FileHandle` 对象。
参见 open(2)。

`mode` 用于设置文件模式（权限和粘滞位），但仅限于创建文件时。

有些字符 (`< > : " / \ | ? *`) 在 Windows 上是预留的，参见[命名文件、路径以及命名空间][Naming Files, Paths, and Namespaces]。
在 NTFS 上，如果文件名包含冒号，则 Node.js 会打开文件系统流，参见[此 MSDN 页面][MSDN-Using-Streams]。

