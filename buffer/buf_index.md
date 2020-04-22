<!-- YAML
type: property
name: [index]
-->

* `index` {integer}

索引操作符 `[index]` 可用于获取或设置 `buf` 中指定的 `index` 位置的八位字节。
该值指向单个字节，所以有效的值的范围是 `0x00` 至 `0xFF`（十六进制）、或 `0` 至 `255`（十进制）。

该操作符继承自 `Uint8Array`，所以对越界访问的行为与 `Uint8Array` 相同。
也就是说，当 `index` 为负数或 `>= buf.length` 时，则 `buf[index]` 返回 `undefined`，而如果 `index` 为负数或 `>= buf.length` 时，则 `buf[index] = value` 不会修改该 buffer。

```js
// 拷贝 ASCII 字符串到 `Buffer`，每次拷贝一个字节。
// （这仅适用于只有 ASCII 字符串。通常，应使用 `Buffer.from()` 来执行此转换。）

const str = 'http://nodejs.cn/';
const buf = Buffer.allocUnsafe(str.length);

for (let i = 0; i < str.length; i++) {
  buf[i] = str.charCodeAt(i);
}

console.log(buf.toString('utf8'));
// 打印: http://nodejs.cn/
```

