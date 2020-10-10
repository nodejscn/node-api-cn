<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `encoding` {string} **默认值:** `'utf8'`。
* 返回: {Promise}

异步的 readlink(2)。
`Promise` 会在成功时解决，且带上 `linkString`。

可选的 `options` 参数可以是字符串（指定字符编码）、或具有 `encoding` 属性（指定用于链接路径的字符编码）的对象。 
如果 `encoding` 被设置为 `'buffer'`，则返回的链接路径会作为 `Buffer` 对象传入。

