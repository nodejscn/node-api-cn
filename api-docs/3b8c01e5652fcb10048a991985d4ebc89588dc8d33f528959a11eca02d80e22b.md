<!-- YAML
added: v0.8.6
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/12562
    description: The `callback` parameter is no longer optional. Not passing
                 it will throw a `TypeError` at runtime.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning with id DEP0013.
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


