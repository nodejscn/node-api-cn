<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `options` {Object|integer}
  * `recursive` {boolean} **默认值:** `false`。
  * `mode` {string|integer} Windows 上不支持。**默认值:** `0o777`。
* 返回: {Promise}

异步地创建目录，然后在成功时解决 `Promise` 且不带参数。


可选的 `options` 参数可以是指定模式（权限和粘滞位）的整数，也可以是具有 `mode` 属性和 `recursive` 属性（指示是否应创建父文件夹）的对象。
当 `path` 是一个已存在的目录时，调用 `fsPromises.mkdir()` 仅在 `recursive` 为 false 时才导致拒绝。

