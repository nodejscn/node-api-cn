<!-- YAML
added: v0.5.3
changes:
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14558
    description: The `%o` and `%O` specifiers are supported now.
-->

* `format` {string} 一个类似 `printf` 的格式字符串。

`util.format()` 方法返回一个格式化后的字符串，使用第一个参数作为一个类似 `printf` 的格式。

第一个参数是一个字符串，包含零个或多个占位符。
每个占位符会被对应参数转换后的值所替换。
支持的占位符有：

* `%s` - 字符串。
* `%d` - 数值（整数或浮点数）。
* `%i` - Integer.
* `%f` - Floating point value.
* `%j` - JSON。如果参数包含循环引用，则用字符串 `'[Circular]'` 替换。
* `%o` - Object. A string representation of an object
  with generic JavaScript object formatting.
  Similar to `util.inspect()` with options `{ showHidden: true, depth: 4, showProxy: true }`.
  This will show the full object including non-enumerable symbols and properties.
* `%O` - Object. A string representation of an object
  with generic JavaScript object formatting.
  Similar to `util.inspect()` without options.
  This will show the full object not including non-enumerable symbols and properties.
* `%%` - 单个百分号（`'%'`）。不消耗参数。

如果占位符没有对应的参数，则占位符不被替换。

```js
util.format('%s:%s', 'foo');
// 返回: 'foo:%s'
```

如果传入 `util.format()` 方法的参数比占位符的数量多，则多出的参数会被强制转换为字符串，然后拼接到返回的字符串，参数之间用一个空格分隔。
Excessive arguments whose
`typeof` is `'object'` or `'symbol'` (except `null`) will be transformed by
`util.inspect()`.

```js
util.format('%s:%s', 'foo', 'bar', 'baz'); // 'foo:bar baz'
```

如果第一个参数不是一个字符串，则 `util.format()` 返回一个所有参数用空格分隔并连在一起的字符串。
每个参数都使用 `util.inspect()` 转换为一个字符串。

```js
util.format(1, 2, 3); // '1 2 3'
```

If only one argument is passed to `util.format()`, it is returned as it is
without any formatting.

```js
util.format('%% %s'); // '%% %s'
```

