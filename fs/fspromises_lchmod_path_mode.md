<!-- YAML
deprecated: v10.0.0
-->

* `path` {string|Buffer|URL}
* `mode` {integer}
* 返回: {Promise}

更改符号链接的权限，然后在成功时解决 `Promise` 且不带参数。
此方法仅在 macOS 上实现。
