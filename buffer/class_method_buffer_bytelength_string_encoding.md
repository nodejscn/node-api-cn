<!-- YAML
added: v0.1.90
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/8946
    description: Passing invalid input will now throw an error.
  - version: v5.10.0
    pr-url: https://github.com/nodejs/node/pull/5255
    description: The `string` parameter can now be any `TypedArray`, `DataView`
                 or `ArrayBuffer`.
-->

* `string` {string|Buffer|TypedArray|DataView|ArrayBuffer} 要计算长度的值
* `encoding` {string} 如果 `string` 是字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {integer} `string` 包含的字节数

返回一个字符串的实际字节长度。
这与 [`String.prototype.length`] 不同，因为那返回字符串的**字符**数。

*注意* 对于 `'base64'` 和 `'hex'`， 该函数假定有效的输入。 对于包含 non-Base64/Hex-encoded 数据的字符串 (e.g. 空格)， 返回值可能大于
从字符串中创建的 `Buffer` 的长度。 

例子：

```js
const str = '\u00bd + \u00bc = \u00be';

// 输出: ½ + ¼ = ¾: 9 个字符, 12 个字节
console.log(`${str}: ${str.length} 个字符, ` +
            `${Buffer.byteLength(str, 'utf8')} 个字节`);
```

当 `string` 是一个 `Buffer`/[`DataView`]/[`TypedArray`]/[`ArrayBuffer`] 时，返回实际的字节长度。

