<!-- YAML
added: v0.11.2
-->

* `path` {string}
* 返回: {boolean}

`path.isAbsolute()` 方法检测 `path` 是否为绝对路径。

如果给定的 `path` 是零长度字符串，则返回 `false`。


例如，在 POSIX 上：

```js
path.isAbsolute('/foo/bar'); // true
path.isAbsolute('/baz/..');  // true
path.isAbsolute('qux/');     // false
path.isAbsolute('.');        // false
```

在 Windows 上：

```js
path.isAbsolute('//server');    // true
path.isAbsolute('\\\\server');  // true
path.isAbsolute('C:/foo/..');   // true
path.isAbsolute('C:\\foo\\..'); // true
path.isAbsolute('bar\\baz');    // false
path.isAbsolute('bar/baz');     // false
path.isAbsolute('.');           // false
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

