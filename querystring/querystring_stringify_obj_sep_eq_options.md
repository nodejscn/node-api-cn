<!-- YAML
added: v0.1.25
-->

* `obj` {Object} 要序列化成一个 URL 查询字符串的对象。
* `sep` {string} 用于界定查询字符串中的键值对的子字符串。默认为 `'&'`。
* `eq` {string} 用于界定查询字符串中的键与值的子字符串。默认为 `'='`。
* `options`
  * `encodeURIComponent` {Function} 当把对 URL 不安全的字符转换成查询字符串中的百分号编码时使用的函数。默认为 `querystring.escape()`。

`querystring.stringify()` 方法通过遍历对象的自有属性，从一个给定的 `obj` 产生一个 URL 查询字符串。

It serializes the following types of values passed in `obj`:
{string|number|boolean|string[]|number[]|boolean[]}
Any other input values will be coerced to empty strings.

例子：

```js
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' });
// 返回 'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({ foo: 'bar', baz: 'qux' }, ';', ':');
// 返回 'foo:bar;baz:qux'
```

默认情况下，查询字符串中需要百分号编码的字符会作为 UTF-8 被编码。
如果需要的是另一种编码，则 `encodeURIComponent` 选项需要被指定，如以下例子：

```js
// 假设 gbkEncodeURIComponent 函数已存在。

querystring.stringify({ w: '中文', foo: 'bar' }, null, null,
  { encodeURIComponent: gbkEncodeURIComponent });
```

