<!-- YAML
added: v0.8.6
-->

* `path` {string|Buffer|URL}
* `len` {integer} **默认值:** `0`。

同步的 truncate(2)。
返回 `undefined`。
文件描述符也可以作为第一个参数传入。 
在这种情况下，调用 `fs.ftruncateSync()`。

不推荐传入文件描述符，可能导致将来抛出错误。


