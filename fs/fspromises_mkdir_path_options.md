<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} 在 Windows 上不支持。**默认值:** `0o777`。
* 返回: {Promise}

异步地创建目录，然后在成功时解决 `Promise`，且不带参数，或者带上创建的第一个目录的路径（如果 `recursive` 为 `true`）。

可选的 `options` 参数可以是整数（指定 `mode`（权限和粘滞位））、或对象（具有 `mode` 属性和 `recursive` 属性（指示是否要创建父目录））。
当 `path` 是已存在的目录时，调用 `fsPromises.mkdir()` 仅在 `recursive` 为 false 时才导致拒绝。

