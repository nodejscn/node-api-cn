<!-- YAML
type: property
name: [index]
-->

索引操作符 `[index]` 可用于获取或设置 `buf` 中指定 `index` 位置的八位字节。
这个值指向的是单个字节，所以合法的值范围是的 `0x00` 至 `0xFF`（十六进制），或 `0` 至 `255`（十进制）。

该操作符继承自 `Uint8Array`，所以它对越界访问的处理与 `UInt8Array` 相同（也就是说，获取时返回 `undefined`，设置时什么也不做）。

例如：拷贝一个 ASCII 字符串到一个 `Buffer`，每次一个字节。

```js
const str = 'Node.js';
const buf = Buffer.allocUnsafe(str.length);

for (let i = 0; i < str.length; i++) {
  buf[i] = str.charCodeAt(i);
}

// 输出: Node.js
console.log(buf.toString('ascii'));
```

