<!-- YAML
added: v0.1.16
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: 传入非字符串作为 `path` 参数会抛出错误。
-->

* `path` {string}
* 返回: {string}

`path.dirname()` 方法会返回 `path` 的目录名，类似于 Unix 的 `dirname` 命令。 
尾部的目录分隔符会被忽略，参见 [`path.sep`]。

```js
path.dirname('/目录1/目录2/目录3');
// 返回: '/目录1/目录2'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

