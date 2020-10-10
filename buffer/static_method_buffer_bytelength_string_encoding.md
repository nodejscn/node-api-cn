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

* `string` {string|Buffer|TypedArray|DataView|ArrayBuffer|SharedArrayBuffer} 要计算长度的值。
* `encoding` {string} 如果 `string` 是字符串，则这是它的字符编码。**默认值:** `'utf8'`。
* 返回: {integer} `string` 中包含的字节数。

当使用 `encoding` 进行编码时，返回字符串的字节长度。
与 [`String.prototype.length`] 不同，后者不会考虑用于将字符串转换为字节的编码。

对于 `'base64'` 和 `'hex'`，此函数会假定输入是有效的。 
对于包含非 base64/hex 编码的数据（例如空格）的字符串，返回值可能是大于从字符串创建的 `Buffer` 的长度。

```js
const str = '\u00bd + \u00bc = \u00be';

console.log(`${str}: ${str.length} 个字符, ` +
            `${Buffer.byteLength(str, 'utf8')} 个字节`);
// 打印: ½ + ¼ = ¾: 9 个字符, 12 个字节
```

当 `string` 是一个 `Buffer`/[`DataView`][]/[`TypedArray`][]/[`ArrayBuffer`][]/[`SharedArrayBuffer`] 时，返回 `.byteLength` 报告的字节长度。

