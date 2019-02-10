<!-- YAML
added: v0.1.16
-->

* `...paths` {string} 路径片段的序列。
* 返回: {string}

`path.join()` 方法使用平台特定的分隔符作为定界符将所有给定的 `path` 片段连接在一起，然后规范化生成的路径。

零长度的 `path` 片段会被忽略。 
如果连接的路径字符串是零长度的字符串，则返回 `'.'`，表示当前工作目录。


```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 返回: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// 抛出 'TypeError: Path must be a string. Received {}'
```

如果任何路径片段不是字符串，则抛出 [`TypeError`]。

