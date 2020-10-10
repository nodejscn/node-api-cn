<!-- YAML
added: v0.8.6
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则在运行时会抛出 `TypeError`。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: 参数 `callback` 不再是可选的。 
      如果不传入，则会触发弃用警告（id 为 DEP0013）。
-->

* `path` {string|Buffer|URL}
* `len` {integer} **默认值:** `0`。
* `callback` {Function}
  * `err` {Error}

异步的 truncate(2)。
除了可能的异常，完成回调没有其他参数。
文件描述符也可以作为第一个参数传入。 
在这种情况下，调用 `fs.ftruncate()`。

不推荐传入文件描述符，可能导致将来抛出错误。


