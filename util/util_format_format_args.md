<!-- YAML
added: v0.5.3
changes:
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/23708
    description: The `%d`, `%f` and `%i` specifiers now support Symbols
                 properly.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: The `format` argument is now only taken as such if it actually
                 contains format specifiers.
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: If the `format` argument is not a format string, the output
                 string's formatting is no longer dependent on the type of the
                 first argument. This change removes previously present quotes
                 from strings that were being output when the first argument
                 was not a string.
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/24806
    description: The `%o` specifier's `depth` has default depth of 4 again.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/17907
    description: The `%o` specifier's `depth` option will now fall back to the
                 default depth.
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/22097
    description: The `%d` and `%i` specifiers now support BigInt.
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14558
    description: The `%o` and `%O` specifiers are supported now.
-->

* `format` {string} 一个类似 `printf` 的格式字符串。

`util.format()` 方法返回一个格式化后的字符串，使用第一个参数作为一个类似 `printf` 的格式的字符串，该字符串可以包含零个或多个格式占位符。
每个占位符会被对应参数转换后的值所替换。
支持的占位符有：

* `%s` - `String` 将用于转换除 `BigInt`、`Object` 和 `-0` 外的所有值。`BigInt` 值将用 `n` 表示，而没有用户定义 `toString` 函数的对象使用带有选项 `{ depth: 0, colors: false, compact: 3 }` 的 `util.inspect()` 进行检查。

* `%d` - `Number` 将用于转换除 `BigInt` 和 `Symbol` 之外的所有值。
* `%i` - `parseInt(value, 10)` 用于除 `BigInt` 和 `Symbol` 之外的所有值。
* `%f` - `parseFloat(value)` 用于除 `BigInt` 和 `Symbol` 之外的所有值。
* `%j` - JSON。如果参数包含循环引用，则替换为字符串 `'[Circular]'`。
* `%o` -  `Object`。具有通用 JavaScript 对象格式的对象的字符串表示形式。 类似于带有选项 `{ showHidden: true, showProxy: true }` 的 `util.inspect()`。 这将显示完整对象，包括非可枚举属性和代理。
* `%O` - `Object`。具有通用 JavaScript 对象格式的对象的字符串表示形式。 类似于 `util.inspect()` 但没有选项。 这将显示完整对象，不包括非可枚举属性和代理。
* `%%` - 单个百分号（`'%'`）。这不会消耗参数。
* 返回: {string} 格式化的字符串。

如果占位符没有对应的参数，则占位符不被替换。

```js
util.format('%s:%s', 'foo');
// 返回: 'foo:%s'
```

如果类型不是 `string`，则使用 `util.inspect()` 格式化不属于格式字符串的值。

如果传入 `util.format()` 方法的参数比占位符的数量多，则多出的参数会被强制转换为字符串，然后拼接到返回的字符串，参数之间用一个空格分隔。

```js
util.format('%s:%s', 'foo', 'bar', 'baz');
// 返回: 'foo:bar baz'
```

如果第一个参数不是一个字符串，则 `util.format()` 返回一个所有参数用空格分隔并连在一起的字符串。

```js
util.format(1, 2, 3);
// 返回: '1 2 3'
```

如果只有一个参数传给 `util.format()`，它将按原样返回，不带任何格式：

```js
util.format('%% %s');
// 返回: '%% %s'
```

`util.format()` 是一种用作调试工具的同步方法。 
某些输入值可能会产生严重的性能开销，从而阻止事件循环。 
请谨慎使用此功能，切勿在热代码路径中使用。

