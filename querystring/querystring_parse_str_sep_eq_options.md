<!-- YAML
added: v0.1.25
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/10967
    description: Multiple empty entries are now parsed correctly (e.g. `&=&=`).
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6055
    description: The returned object no longer inherits from `Object.prototype`.
  - version: v6.0.0, v4.2.4
    pr-url: https://github.com/nodejs/node/pull/3807
    description: The `eq` parameter may now have a length of more than `1`.
-->

* `str` {string} 要解析的 URL 查询字符串。
* `sep` {string} 用于界定查询字符串中的键值对的子字符串。默认为 `'&'`。
* `eq` {string} 用于界定查询字符串中的键与值的子字符串。默认为 `'='`。
* `options` {Object}
  * `decodeURIComponent` {Function} 解码查询字符串的字符时使用的函数。默认为 `querystring.unescape()`。
  * `maxKeys` {number} 指定要解析的键的最大数量。默认为 `1000`。指定为 `0` 则不限制。

该方法会把一个 URL 查询字符串 `str` 解析成一个键值对的集合。

例子，查询字符串 `'foo=bar&abc=xyz&abc=123'` 被解析成：

<!-- eslint-skip -->
```js
{
  foo: 'bar',
  abc: ['xyz', '123']
}
```

该方法返回的对象不继承自 JavaScript 的 `Object` 类。
这意味着 `Object` 类的方法如 `obj.toString()`、`obj.hasOwnProperty()` 等没有被定义且无法使用。

默认情况下，查询字符串中的字符会被视为使用 UTF-8 编码。
如果使用的是其他字符编码，则需要指定 `decodeURIComponent` 选项，例如：

```js
// 假设存在 gbkDecodeURIComponent 函数。
querystring.parse('w=%D6%D0%CE%C4&foo=bar', null, null,
                  { decodeURIComponent: gbkDecodeURIComponent });
```

