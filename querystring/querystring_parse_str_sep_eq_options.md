<!-- YAML
added: v0.1.25
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10967
    description: 现在可以正确地解析多个空的条目（例如 `&=&=`）。
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6055
    description: 返回的对象不再继承自 `Object.prototype`。
  - version: v6.0.0, v4.2.4
    pr-url: https://github.com/nodejs/node/pull/3807
    description: 参数 `eq` 现在可以长度大于 `1`。
-->

* `str` {string} 要解析的 URL 查询字符串。
* `sep` {string} 用于在查询字符串中分隔键值对的子字符串。**默认值:** `'&'`。
* `eq` {string} 用于在查询字符串中分隔键和值的子字符串。**默认值:** `'='`。
* `options` {Object}
  * `decodeURIComponent` {Function} 当解码查询字符串中的百分比编码字符时使用的函数。**默认值:** `querystring.unescape()`。
  * `maxKeys` {number} 指定要解析的键的最大数量。指定 `0` 可移除键的计数限制。**默认值:** `1000`。

`querystring.parse()` 方法将 URL 查询字符串 `str` 解析为键值对的集合。

例如，查询字符串 `'foo=bar&abc=xyz&abc=123'` 会被解析为：


<!-- eslint-skip -->
```js
{
  foo: 'bar',
  abc: ['xyz', '123']
}
```

`querystring.parse()` 方法返回的对象不是原型地继承自 JavaScript 的 `Object`。
这意味着典型的 `Object` 方法如 `obj.toString()`、`obj.hasOwnProperty()` 等都没有被定义并且不起作用。

默认情况下，会假定查询字符串中的百分比编码字符使用 UTF-8 编码。
如果使用其他的字符编码，则需要指定其他的 `decodeURIComponent` 选项：

```js
// 假设 gbkDecodeURIComponent 函数已存在。

querystring.parse('w=%D6%D0%CE%C4&foo=bar', null, null,
                  { decodeURIComponent: gbkDecodeURIComponent });
```

