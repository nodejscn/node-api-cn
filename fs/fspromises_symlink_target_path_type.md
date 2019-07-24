<!-- YAML
added: v10.0.0
-->

* `target` {string|Buffer|URL}
* `path` {string|Buffer|URL}
* `type` {string} **默认值:** `'file'`。
* 返回: {Promise}

创建一个符号链接，然后在成功时解决 `Promise` 且不带参数。

`type` 参数仅在 Windows 上可用，可以是 `'dir'`、`'file'` 或 `'junction'` 之一。 
Windows 上使用 `'junction'` 要求目标路径是绝对路径。 
当使用 `'junction'` 时，`target` 参数将自动标准化为绝对路径。

