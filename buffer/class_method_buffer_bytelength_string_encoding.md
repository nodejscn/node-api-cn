<!-- YAML
added: v0.1.90
-->

* `string` {String | Buffer | TypedArray | DataView | ArrayBuffer} 要计算长度的值
* `encoding` {String} 如果 `string` 是字符串，则这是它的字符编码。
  **默认:** `'utf8'`
* 返回: {Integer} `string` 包含的字节数

返回一个字符串的实际字节长度。
这与 [`String.prototype.length`] 不同，因为那返回字符串的**字符**数。

例子：

```js
const str = '\u00bd + \u00bc = \u00be';

// 输出: ½ + ¼ = ¾: 9 个字符, 12 个字节
console.log(`${str}: ${str.length} 个字符, ` +
            `${Buffer.byteLength(str, 'utf8')} 个字节`);
```

当 `string` 是一个 `Buffer`/[`DataView`]/[`TypedArray`]/[`ArrayBuffer`] 时，返回实际的字节长度。

否则，会转换为 `String` 并返回字符串的字节长度。

