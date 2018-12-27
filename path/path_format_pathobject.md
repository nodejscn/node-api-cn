<!-- YAML
added: v0.11.15
-->

* `pathObject` {Object}
  * `dir` {string}
  * `root` {string}
  * `base` {string}
  * `name` {string}
  * `ext` {string}
* 返回: {string}

将一个对象格式化为一个路径字符串。
与 [`path.parse()`] 相反。

`pathObject` 的属性有不同的优先级：

* 如果指定了 `pathObject.dir`，则忽略 `pathObject.root`。
* 如果指定了 `pathObject.base`，则忽略 `pathObject.ext` 和 `pathObject.name`。

例如，在 POSIX 上：

```js
// 如果指定了 `dir`、`root` 和 `base`，则返回 `${dir}${path.sep}${base}`。
// `root` 会被忽略。
path.format({
  root: '/ignored',
  dir: '/home/user/dir',
  base: 'file.txt'
});
// 返回: '/home/user/dir/file.txt'

// 如果没有指定 `dir`，则使用 `root`。
// 如果只指定了 `root` 或 `dir` 等于 `root`，则不会包含分隔符。
// `ext` 会被忽略。
path.format({
  root: '/',
  base: 'file.txt',
  ext: 'ignored'
});
// 返回: '/file.txt'

// 如果没有指定 `base`，则使用 `name` + `ext`。
path.format({
  root: '/',
  name: 'file',
  ext: '.txt'
});
// 返回: '/file.txt'
```

在 Windows 上：

```js
path.format({
  dir: 'C:\\path\\dir',
  base: 'file.txt'
});
// 返回: 'C:\\path\\dir\\file.txt'
```

