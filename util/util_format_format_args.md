<!-- YAML
added: v0.5.3
changes:
  - version: v12.11.0
    pr-url: https://github.com/nodejs/node/pull/29606
    description: 说明符 `%c` 现在是忽略的。
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: 参数 `format` 现在仅在其实际包含格式说明符时才被采用。
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/23162
    description: 如果 `format` 参数不是一个格式字符串，则输出字符串的格式化不再依赖于第一个参数的类型。
      当第一个参数不是一个字符串时，此更改会从正在被输出的字符串中移除先前存在的引号。
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/23708
    description: 说明符 `%d`、`%f` 和 `%i` 现在正确地支持符号。
  - version: v11.4.0
    pr-url: https://github.com/nodejs/node/pull/24806
    description: 说明符 `%o` 的 `depth` 再次具有默认的深度 4。
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/17907
    description: 说明符 `%o` 的 `depth` 选项现在会回退到默认的深度。
  - version: v10.12.0
    pr-url: https://github.com/nodejs/node/pull/22097
    description: 说明符 `％d` 和 `％i` 现在支持 BigInt。
  - version: v8.4.0
    pr-url: https://github.com/nodejs/node/pull/14558
    description: 说明符 `％o` 和 `％O` 现在是支持的。
-->

* `format` {string} 一个类似 `printf` 的格式字符串。

`util.format()` 方法使用第一个参数作为一个类似 `printf` 的格式字符串（可以包含零个或者多个格式说明符）返回一个格式化后的字符串。
每个说明符被从对应的参数转换后的值所替换。
支持的说明符有：

* `%s`：`String` 会被用于转换除 `BigInt`、`Object` 和 `-0` 之外的所有值。
        `BigInt` 值会被使用一个 `n` 表示，而不具有用户定义的 `toString` 函数的对象会被使用具有 `{ depth: 0, colors: false, compact: 3 }` 选项的 `util.inspect()` 检查。
* `%d`：`Number` 会被用于转换除 `BigInt` 和 `Symbol` 之外的所有值。
* `%i`：`parseInt(value, 10)` 被用于除 `BigInt` 和 `Symbol` 之外的所有值。
* `%f`：`parseFloat(value)` 被用于除 `Symbol` 之外的所有值。
* `%j`：JSON。如果参数包含循环的引用，则使用字符串 `'[Circular]'` 替换。
* `%o`：`Object`。一个具有通用的 JavaScript 对象格式的对象的字符串表示。 
        类似于具有 `{ showHidden: true, showProxy: true }` 选项的 `util.inspect()`。 
	这会展示完整的对象，包括不可枚举的属性和代理。
* `%O`：`Object`。一个具有通用的 JavaScript 对象格式的对象的字符串表示。 
        类似于没有选项的 `util.inspect()`。
	这会展示完整的对象，不包括不可枚举的属性和代理。
* `%c`：`CSS`。此说明符是忽略的，并且会跳过任何传入的 CSS。
* `%%`：单个百分号（`'%'`）。这不会消费一个参数。
* 返回: {string} 格式化的字符串。

如果一个说明符不具有一个对应的参数，则它不被替换。

```js
util.format('%s:%s', 'foo');
// 返回: 'foo:%s'
```

如果其类型不是 `string`，则不属于格式字符串的值被使用 `util.inspect()` 格式化。

如果传给 `util.format()` 方法的参数比说明符的数量多，则多出的参数被连接到返回的字符串，被空格分隔。

```js
util.format('%s:%s', 'foo', 'bar', 'baz');
// 返回: 'foo:bar baz'
```

如果第一个参数不包含一个有效的格式说明符，则 `util.format()` 返回一个所有的参数被空格分隔的连接的字符串。

```js
util.format(1, 2, 3);
// 返回: '1 2 3'
```

如果只有一个参数被传给 `util.format()`，则它被原样返回，不进行任何格式化：

```js
util.format('%% %s');
// 返回: '%% %s'
```

`util.format()` 是一个旨在被作为一个调试工具的同步方法。 
一些输入值可能具有一个严重的性能开销，从而可能阻止事件循环。 
使用此函数需谨慎，并且不要在一个热代码路径中。

