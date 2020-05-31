<!-- YAML
added: v0.1.25
changes:
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/5348
    description: 传入非字符串作为 `path` 参数会抛出错误。
-->

* `path` {string}
* `ext` {string} 可选的文件扩展名。
* 返回: {string}

`path.basename()` 方法会返回 `path` 的最后一部分，类似于 Unix 的 `basename` 命令。 
尾部的目录分隔符会被忽略，参见 [`path.sep`]。


```js
path.basename('/目录1/目录2/文件.html');
// 返回: '文件.html'

path.basename('/目录1/目录2/文件.html', '.html');
// 返回: '文件'
```

如果 `path` 不是字符串、或给定了 `ext` 但不是字符串，则抛出 [`TypeError`]。

