<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `len` {integer} **默认值:** `0`。
* 返回: {Promise}

截断 `path`，然后在成功时解决 `Promise` 且不带参数。
`path` 必须是一个字符串或 `Buffer`。

