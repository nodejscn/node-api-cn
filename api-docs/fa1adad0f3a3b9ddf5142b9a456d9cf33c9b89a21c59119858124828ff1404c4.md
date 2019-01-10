<!-- YAML
added: v0.1.16
-->

* `...paths` {string} 路径片段。
* 返回: {string}

使用平台特定的分隔符把所有 `path` 片段连接到一起，并规范化生成的路径。

空字符串的 `path` 片段会被忽略。
如果连接后的路径是一个空字符串，则返回 `'.'`，表示当前工作目录。

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
// 返回: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar');
// 抛出 'TypeError: Path must be a string. Received {}'
```

如果 `path` 不是字符串，则抛出 [`TypeError`]。

