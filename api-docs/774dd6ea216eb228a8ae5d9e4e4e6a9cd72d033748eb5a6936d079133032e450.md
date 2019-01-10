<!-- YAML
added: v0.1.25
-->

* `obj` {Object} 要序列化成 URL 查询字符串的对象。
* `sep` {string} 用于界定查询字符串中的键值对的子字符串。默认为 `'&'`。
* `eq` {string} 用于界定查询字符串中的键与值的子字符串。默认为 `'='`。
* `options`
  * `encodeURIComponent` {Function} 把对象中的字符转换成查询字符串时使用的函数。默认为 `querystring.escape()`。

该方法通过遍历给定的 `obj` 对象的自身属性，生成 URL 查询字符串。

如果 `obj` 对象中的属性的类型为 {string|number|boolean|string[]|number[]|boolean[]}，则属性的值会被序列化。
其他类型的属性的值会被强制转换为空字符串。

例子：

```js
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' });
// 返回 'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({ foo: 'bar', baz: 'qux' }, ';', ':');
// 返回 'foo:bar;baz:qux'
```

默认情况下，使用 UTF-8 进行编码。
如果需要使用其他编码，则需要指定 `encodeURIComponent` 选项，例如：

```js
// 假设存在 gbkEncodeURIComponent 函数。
querystring.stringify({ w: '中文', foo: 'bar' }, null, null,
                      { encodeURIComponent: gbkEncodeURIComponent });
```

