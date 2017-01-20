<!-- YAML
added: v0.1.90
-->

* `string` {String} 要写入 `buf` 的字符串
* `offset` {Integer} 开始写入 `string` 的位置。**默认:** `0`
* `length` {Integer} 要写入的字节数。**默认:** `buf.length - offset`
* `encoding` {String} `string` 的字符编码。**默认:** `'utf8'`
* 返回: {Integer} 写入的字节数

根据 `encoding` 的字符编码写入 `string` 到 `buf` 中的 `offset` 位置。
`length` 参数是写入的字节数。
如果 `buf` 没有足够的空间保存整个字符串，则只会写入 `string` 的一部分。
只部分解码的字符不会被写入。

例子：

```js
const buf = Buffer.allocUnsafe(256);

const len = buf.write('\u00bd + \u00bc = \u00be', 0);

// 输出: 12 个字节: ½ + ¼ = ¾
console.log(`${len} 个字节: ${buf.toString('utf8', 0, len)}`);
```

